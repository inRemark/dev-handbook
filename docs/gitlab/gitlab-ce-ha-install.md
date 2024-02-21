# GitLab CE HA Install



## 文档介绍
### 引言

GitLab是一个基于Web的Git存储库，它提供免费的开放和私有存储库、问题跟踪功能和wiki。它是一个完整的DevOps平台，使专业人员能够执行项目中的所有任务——从项目计划和源代码管理到监控和安全。

为了更好标准化Gitlab 安装配置规范，满足项目需求，特编写此文档

### 适用范围

本文档适用于Linux操作系统下对于Gitlab 服务搭建及相关组件的高可用配置

### 实施建议

建议实施人员先完整阅读本文档和官方高可用配置文档：https://docs.gitlab.com/ee/administration/reference_architectures/3k_users.html

## 高可用架构和组件介绍


### 官方系统架构图

![GitLab系统架构](https://docs.gitlab.com/ee/development/img/architecture_simplified_v14_9.png)

### 官方高可用架构

![GitLab高可用架构图](https://plantuml.gitlab-static.net/png/U9nzLijk6Z4KtVihhCnkMW8DA2IRA0L2L2bgQLYs21d6W8kngUrHWwh-U_qQpyDkLp3ttCUvnxvtvb4g95Hved1u1F98s1a9T8AKCAmkPmovK0SEm1Q90bxb-TERme8X2byuAk04KSIsMEJv5KGIOhg1sIswt-1n2FZ4_XD0JC3zS3oOJG1GV8_L0Glu6q2uvPJYhIASIPFbcQWNj86lY52Pv_1jQCFtH55jpOOtqzdm9evQaW8VoKyJCB81qXbWjjlT5SK7yATRrPDU27uorbB2T_1Pe1rYo5C-SKOK5p0Rp-VpsIWkEjM_9Qr9RkqppF3OA6DAkYgw9KGlS4fBgHMg-j6czTQPKZei1C8x_LodFtiBpERpk-bWaDHEPssfPWet_4FNFjM2IxKNUFdr9S_pxwpV_ymPtA6IgfxY50l4LB_Vghu-kn0PqkgyWLhlcxUkUW--V1f-Y1FMWisGGXiaiIrS-8UaICyJNhfR5bJQRvm9PgEdZ_heccqtkeNz_aAG4nANga5FOtrsvcPyfsexpHBhWozi8lXsqyubAonaCt84YbeFPpPoTGaOpowdwn3ma2XIA_YA2o8j5M7-fRIpBhLkrc_DUE5EzdOu6jjqb9TMko-R7-O4bteYq1xx4U7Mk9RE2BDV1w8m06OxwDRSVl0tGOzls_wUwI1sNFKqxaSD03_dsibDUjD9hv08NmaDj5d4FhsU2RSDLk1r1wmkMHry84M1sQf1BW6vYGUWsZQwfjitNTwHGufuxDHaNg7N7JHGhyDZxYci8a_SgRZbR1ctjrF28THqK9KpS6sPoxfMP0y7xtUdRivjJulwQvF4V4SnA1ff8x39FGLsEk-wD8_LTGggjuJsSU-99lCqM56FqI1K33MP9z4EzSWdvfwgRoxhFqDB4wk76817p0hz9G7-0k8PguG0)


### 组件介绍

**Git** 

用来调用Git相关功能

**Nginx负载均衡**
分为外部负载均衡器和内部负载均衡器，以处理GitLab应用程序服务节点外部与内部连接的负载平衡。

**Redis+sentinel**

Gitlab服务所依赖的缓存服务

**Consul&Patroni&PostgreSQL**

PostgreSQL数据库高可用组件。

**PgBouncer**

PostgreSQL的连接池服务。

**Gitlay**

提供对Git存储库的访问。

**Sidekiq**

后台任务处理服务

**Gitlab Rails**

用以运行Puma、Workhorse、GitLab Shell，并服务于所有前端请求
（包括通过HTTP/SSH的UI、API和Git）。

**Prometheus + Grafana（可选）**

GitLab环境及相关指标监控。

**Elastic search（可选）**

配置用以在整个GitLab实例中进行更快、更高级的代码搜索。

**对象存储/NFS（可选）**

用以存放各种二进制文件或对象（推荐使用对象存储）


## 系统环境和节点配置


### 系统要求

>CPU：8 core
Mem：16GB
Disk：不低于20G
带宽：100Mbps
操作系统版本：Centos 7/8/9

### 组件的安装

本文档中所有安装的服务均基于二进制安装，安装目录在/opt/gitlab/<对应的服务组件名称>/下
安装包均上传至 ***~/root/gitlab-install/*** 中作为统一介质存储目录

### 节点资源


|IP             |服务组件               |备注                 |
|---------------|----------------------|--------------------|
|192.168.0.100   |nginx                |负载均衡器
|192.168.0.1    |gitaly praefect gitlab rails sidekiq  |
|192.168.0.2    |gitaly praefect gitlab rails sidekiq  |
|192.168.0.3    |gitaly praefect gitlab rails sidekiq  |
|192.168.0.10   |PostgreSQL Patroni Pgbouncer consul-client|
|192.168.0.11   |PostgreSQL Patroni Pgbouncer consul-client|
|192.168.0.12   |PostgreSQL Patroni Pgbouncer consul-client|
|192.168.0.20   |consul redis sentinel|
|192.168.0.21   |consul redis sentinel|
|192.168.0.22   |consul redis sentinel|



## 操作系统初始化


### 添加用户

添加用户
```
useradd gitlab -d /opt/gitlab
```

为用户gitlab赋予/opt/gitlab目录权限
```
chown -R gitlab /opt/gitlab
```

### 安装依赖

```
yum install -y build-essential zlib1g-dev libyaml-dev libssl-dev libgdbm-dev libre2-dev \
  libreadline-dev libncurses5-dev libffi-dev curl openssh-server libxml2-dev libxslt-dev \
  libcurl4-openssl-dev libicu-dev logrotate rsync python3-docutils pkg-config cmake runit-systemd
```

### 声明字符集（可选）

```
export LC_ALL="en_US.UTF-8"
export LC_CTYPE="en_US.UTF-8"
```


## 安装GitLab CE


### 下载Gitlab CE介质

介质包含NGINX, Postgres, Redis等组件包，根据需要在[https://packages.gitlab.com/gitlab/gitlab-ce](https://packages.gitlab.com/gitlab/gitlab-ce)选择合适的rpm包，本文档中使用如下


```
#确认系统版本
uname -a
cat /etc/redhat-release

CentOS8资源包
wget --content-disposition https://packages.gitlab.com/gitlab/gitlab-ee/packages/el/8/gitlab-ee-15.4.2-ce.0.el8.x86_64.rpm/download.rpm

CentOS7资源包
wget --content-disposition https://packages.gitlab.com/gitlab/gitlab-ee/packages/el/7/gitlab-ee-15.4.2-ce.0.el7.x86_64.rpm/download.rpm

```

### 执行安装

**在所有gitlab节点上执行安装**

```
rpm -ivh [download].rpm
```

### 卸载Gitlab服务

1、停止 gitlab服务
gitlab-ctl stop

2、卸载 gitlab（社区版）
rpm -e gitlab-ce

3、查看 gitlab 进程
ps aux | grep gitlab

4、杀掉gitlab service进程(其实就是强杀/opt/gitlab/service进程)
kill -9 xxxxxx

5、删除所有包含 gitlab 的遗留文件
find / -name gitlab

6、删除所有包含gitlab文件
find / -name gitlab | xargs rm -rf


### 可能遇到问题

**Centos7提示缺包，按提示安装即可**
```
Q1. 
	policycoreutils-python-utils is needed by gitlab-ee-15.4.2-ee.0.el8.x86_64
	policycoreutils-python is needed by gitlab-ee-15.4.2-ee.0.el8.x86_64
A1. yum install policycoreutils-python 或者policycoreutils-python-utils
```


**卸载重装卡住问题**

```
# kill然后执行：
systemctl restart gitlab-runsvdir
```


## Consul&Redis&Sentinel集群

使用外部consul
使用外部redis


## GitLab配置

### GitLab服务组件开关

```
consul['enable'] = false # for GitLab EE
redis['enable'] = false
postgresql['enable'] = false
gitlab_kas['enable'] = false
alertmanager['enable'] = false
prometheus['enable'] = false
grafana['enable'] = false
gitlab_exporter['enable'] = false

gitaly['enable'] = true
praefect['enable'] = true
puma['enable'] = true
gitlab_workhorse['enable'] = true
sidekiq['enable'] = true
nginx['enable'] = true
```

### Redis

```
# Redis
redis['master_name'] = 'mymaster'
redis['master_password'] = 'pwd@redis'
gitlab_rails['redis_sentinels'] = [
   {'host' => '192.168.0.20', 'port' => '26379'},
   {'host' => '192.168.0.21', 'port' => '26379'},
   {'host' => '192.168.0.22', 'port' => '26379'},
]

```

### Gitaly

```
gitlab_rails['internal_api_url'] = 'http://192.168.0.100:8080'
gitaly['configuration'] = {
    listen_addr: '0.0.0.0:8075',
    #prometheus_listen_addr: '0.0.0.0:9236',
    auth: {
        token: 'Ofgit49token',
        #transitioning: true,
    },
    storage: [
        {
           name: 'gitaly-1', # gitaly-2 gitaly-3
           path: '/var/opt/gitlab/git-data',
        }
    ],
    # 包对象缓存 默认为false
    pack_objects_cache: {
        # ...
        enabled: true,
        # 默认不需要配置
        # dir: '/var/opt/gitlab/git-data/repositories/+gitaly/PackObjectsCache',
        # max_age: '5m',
        # min_occurrences: 1,
    },

    # for 16.x.x
    hooks: {
        # gitaly['custom_hooks_dir']
        custom_hooks_dir: '/var/opt/gitlab/gitaly/custom_hooks',
    },
}

```

**存储目录配置**

```bash
# on node1
storage: [
    {
        name: 'gitaly-1', 
        path: '/var/opt/gitlab/git-data',
    }
],

# on node2
storage: [
    {
        name: 'gitaly-2',
        path: '/var/opt/gitlab/git-data',
    }
],

# on node3
storage: [
    {
        name: 'gitaly-3',
        path: '/var/opt/gitlab/git-data',
    }
],

```

### Praefect

```
praefect['auto_migrate'] = false
praefect['configuration'] = {
    # ...
    listen_addr: '0.0.0.0:2305',
    auth: {
        # ...
        token: 'Ofgit49token',
    },
        # ...
        database: {
            # ...
            host: '192.168.0.100', # PGBOUNCER_HOST or SLB HOST
            port: 6432,
            user: 'praefect',
            password: 'praefect',
            dbname: 'praefect_production',
            # sslmode: '...',
            # sslcert: '...',
            # sslkey: '...',
            # sslrootcert: '...',
        },
        virtual_storage: [
        {
            # ...
            name: 'default',
            node: [
               {
                  storage: 'gitaly-1',
                  address: 'tcp://192.168.0.1:8075',
                  token: 'Ofgit49token'
               },
               {
                  storage: 'gitaly-2',
                  address: 'tcp://192.168.0.2:8075',
                  token: 'Ofgit49token'
               },
               {
                  storage: 'gitaly-3',
                  address: 'tcp://192.168.0.3:8075',
                  token: 'Ofgit49token'
              },
            ],
        }
    ],
}

```

### GitLab Rails

```
gitlab_rails['auto_migrate'] = false
external_url 'http://192.168.0.100:8080'
gitlab_rails['gitlab_shell_ssh_port'] = 2244
# git_data_dirs get configured for the Praefect virtual storage
# Address is Internal Load Balancer for Praefect
# Token is praefect_external_token
git_data_dirs({
  "default" => {
    "gitaly_address" => "tcp://192.168.0.100:2305", # internal load balancer IP
    "gitaly_token" => 'Ofgit49token'
  }
})
gitlab_rails['db_host'] = '192.168.0.100' # internal load balancer IP
gitlab_rails['db_port'] = 6432
gitlab_rails['db_password'] = 'gitlab'
#gitlab_rails['gitlab_default_can_create_group'] = false
gitlab_rails['gitlab_username_changing_enabled'] = false
puma['listen'] = '0.0.0.0'

```

### Email SMTP（可选）

```
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = 'pop3.oamail.163.cn'
gitlab_rails['smtp_port'] = '25'
gitlab_rails['smtp_user_name'] = 'admin@admin.com'
gitlab_rails['smtp_password'] = 'pwd@pop3'
gitlab_rails['smtp_domain'] = 'mail.163.cn'
gitlab_rails['smtp_authentication'] = 'login'
#gitlab_rails['smtp_enable)starttls_auto'] = ture
gitlab_rails['smtp_tls'] = true
```
### Email Income（可选）
```
gitlab_rails['gitlab_email_from'] = 'pop3.mail.163.cn'
```


### Assets Storage（可选）
gitlab_rails['object_store']['enabled'] = true
gitlab_rails['object_store']['proxy_download'] = true
gitlab_rails['object_store']['connection'] = {
	'provider' =>  'AWS',
	'region' => 'cn-beijing',
	'endpoint' => 'http://192.168.0.200:8000',
	'aws_access_key_id' => '',
	'aws_secret_access_key' => ''
}

gitlab_rails['object_store']['objects']['artifacts']['bucket'] = 'artfacts'
gitlab_rails['object_store']['objects']['external_diffs']['bucket'] = 'external-diffs'
gitlab_rails['object_store']['objects']['lfs']['bucket'] = 'lfs'
gitlab_rails['object_store']['objects']['uploads']['bucket'] = 'uploads'
gitlab_rails['object_store']['objects']['packages']['bucket'] = 'packages'
gitlab_rails['object_store']['objects']['dependency_proxy']['bucket'] = 'dependency-proxy'
gitlab_rails['object_store']['objects']['terraform_state']['bucket'] = 'terraform-state'
gitlab_rails['object_store']['objects']['pages']['bucket'] = 'pages'


### Backup Setting
gitlab_rails['backup_keep_time'] = 259200
gitlab_rails['backup_path'] = '/tmp/gitlab-backups'


### GitLab Nginx
```
nginx['listen_port'] = 8080
```


### Logging
logrotate['enable'] = true
logging['logrotate_frequency'] = "daily"
logging['logrotate_maxsize'] = nil
logging['logrotate_size'] = nil
logging['logrotate_rotate'] = 30 $ keep 30 rotated logs
logging['logrotate_compress'] = "compress"
logging['logrotate_method'] = "copytruncate"
logging['logrotate_postrotate'] = nil
logging['logrotate_dateformat'] = nil 


### Monitoring

Set the network addresses that the exporters uses for monitoring will listen on

```
node_exporter['listen_address'] = '0.0.0.0:9100'
gitlab_exporter['enable'] = true
redis_exporter['listen_address'] = '0.0.0.0:9121'
```

### 常用指令
```
gitlab-ctl reconfigure
gitlab-ctl start
gitlab-ctl stop
gitlab-ctl restart
gitlab-ctl restart praefect
gitlab-ctl tail
gitlab-ctl tail gitaly
```

### 验证和检查

**核实 Praefect 可联通PostgreSQL**
```
sudo -u git /opt/gitlab/embedded/bin/praefect -config /var/opt/gitlab/praefect/config.toml sql-ping
```

**核实每个Gitaly节点的Git hooks可以连通GitLab**
在每个Gitaly节点执行：
```
sudo /opt/gitlab/embedded/bin/gitaly check /var/opt/gitlab/gitaly/config.toml
```

**核实GitLab可连通Praefect**
在每个Praefect节点执行：
```
sudo /opt/gitlab/embedded/bin/praefect -config /var/opt/gitlab/praefect/config.toml dial-nodes
```

**检查Gitaly健康状态**
```
gitlab-rake gitlab:gitaly:check
```

### 验证Praefect&Gitaly

确定Gitaly集群的运行状况
```
gitlab-ctl praefect check
```

## 官方文档参考

### 全部默认端口号
https://docs.gitlab.com/ee/administration/package_information/defaults.html

### 官方高可用配置
https://docs.gitlab.com/ee/administration/reference_architectures/3k_users.html

### PG高可用
https://docs.gitlab.com/15.4/ee/administration/postgresql/replication_and_failover.html#pgbouncer-information

https://docs.gitlab.com/ee/administration/postgresql/replication_and_failover.html#switching-from-repmgr-to-patroni

### PG升级
https://docs.gitlab.com/omnibus/settings/database.html


### Gitaly
https://docs.gitlab.com/ee/administration/gitaly/praefect.html#setup-instructions

https://docs.gitlab.com/ee/install/installation.html#install-gitaly

https://docs.gitlab.com/ee/administration/gitaly/configure_gitaly.html

https://archives.docs.gitlab.com/15.11/ee/administration/gitaly/praefect.html#gitaly

### Gitaly写入异常

https://docs.gitlab.com/ee/administration/gitaly/troubleshooting.html#relation-does-not-exist-errors

### 配置GitLab Rails
https://docs.gitlab.com/ee/administration/reference_architectures/3k_users.html#configure-gitlab-rails

### 配置Prometheus

https://docs.gitlab.com/ee/administration/reference_architectures/3k_users.html#configure-prometheus

### 配置对象存储

https://docs.gitlab.com/ee/administration/reference_architectures/3k_users.html#configure-prometheus

### 配置高级搜索

https://docs.gitlab.com/ee/administration/reference_architectures/3k_users.html#configure-advanced-search

### GiLab 16.x变更

https://docs.gitlab.com/ee/update/versions/gitlab_16_changes.html
