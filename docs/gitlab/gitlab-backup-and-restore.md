# GitLab backup and restore

## 1. 备份恢复主要步骤

- 通知人员暂停使用，进入维护状态
- GitLab健康状态检查
- 备份
- 备份传输
- 恢复机密和配置文件
- 恢复主要数据

## 1.1 GitLab健康状态检查

在备份恢复之前和之后检查GitLab，以确保 GitLab 的主要组件正常工作：

### 1.1.1 检查一般配置

```shell
gitlab-rake gitlab:check
```

官方参考文档
<https://docs.gitlab.com/ee/administration/raketasks/maintenance.html#check-gitlab-configuration>

### 1.1.2 确认加密的数据库值可以解密

```shell
sudo gitlab-rake gitlab:doctor:secrets
```

### 1.1.3 检查GitLab功能特性

- 用户可以登录;
- 项目列表可见;
- 项目问题和合并请求是可访问的;
- 用户可以从 GitLab 克隆存储库;
- 用户可以将提交推送到 GitLab;

### 1.1.4 检查GitLab CI/CD

- Runner 可以获得任务;
- Docker 镜像可以从注册表中推送和拉取（可选）。

### 1.1.5 检查Geo（可选）

请在主数据库和每个辅助数据库上运行相关检查

```shell
sudo gitlab-rake gitlab:geo:check
```

### 1.1.6 检查Elasticsearch（可选）

## 1.2 GitLab 备份

### 1.2.1 创建 GitLab 及其所有数据（数据库、存储库、上传、构建、工件、LFS 对象、注册表、页面）的备份。这对于在升级出现问题时将 GitLab 回滚到工作状态至关重要

### 1.2.2 需要备份的数据

- PostgreSQL databases
- Git repositories
- Blobs
- Container Registry
- Configuration files
- Other data

### 1.2.3 备份步骤

***执行备份***

```shell
sudo gitlab-backup create > /tmp/backup_man_20231111.log
# 备份之后备份文件所在位置 /var/opt/gitlab/backups/
```

***备份配置文件***

```shell
gitlab-ctl backup-etc && cd /etc/gitlab/config_backup
```

**备份检查**
检查备份日志，看是否有异常数据，如果有则排除异常，重新备份

**官方文档参考**
<https://docs.gitlab.com/ee/administration/backup_restore/index.html>

<https://docs.gitlab.com/ee/administration/backup_restore/backup_gitlab.html#storing-configuration-files>

**创建实例的快照（可选）**

如果这是多节点安装，则必须为每个节点创建快照。 此过程超出了 GitLab 支持范围。

## 1.3 备份数据传输或存储

通过任意方式将备份文件传输至新应用主机

## 1.4 GitLab 恢复

### 1.4.1先决条件

- 实例已经运行;
- 目标实例和备份版本相同;

### 1.4.2 恢复secrets

```
/etc/gitlab/gitlab-secrets.json
```

### 1.4.3 恢复 GitLab

**先决条件**
安装的GitLab版本和类型（CE/EE）与创建备份时使用的版本和类型完全相同。

您至少运行过一次sudo gitlab ctl reconfigure。
GitLab正在运行。如果没有，请使用sudogitlabctl-start启动它。
首先确保您的备份tar文件位于gitlab.rb配置gitlab_rails['backup_path']中描述的备份目录中。默认值为/var/opt/gitlab/backups。备份文件需要归git用户所有。

**修改备份文件用户**

```
sudo cp 11493107454_2018_04_25_10.6.4-ce_gitlab_backup.tar /var/opt/gitlab/backups/
sudo chown git:git /var/opt/gitlab/backups/11493107454_2018_04_25_10.6.4-ce_gitlab_backup.tar
```

**停止连接到数据库的进程。让GitLab的其余部分继续运行**

```
sudo gitlab-ctl stop puma
sudo gitlab-ctl stop sidekiq
# 核实验证
sudo gitlab-ctl status
```

**注意事项

>此命令将覆盖GitLab数据库的内容！
注意：名称中省略了“_gitlab_backup.tar”

**执行恢复**

```
# export GITLAB_ASSUME_YES=1
sudo gitlab-backup restore BACKUP=11493107454_2018_04_25_10.6.4-ce
```

**恢复检查**

检查恢复记录日志看是否有异常，如果有，排除异常，重新执行上一步，配置数据库端口等

**重启和检查**

```
sudo gitlab-ctl restart
sudo gitlab-rake gitlab:check SANITIZE=true
```

**在GitLab 13.1及更高版本中，检查数据库值可以解密**

```
sudo gitlab-rake gitlab:doctor:secrets
```

**对上传的文件进行完整性检查**

```
sudo gitlab-rake gitlab:artifacts:check
sudo gitlab-rake gitlab:lfs:check
sudo gitlab-rake gitlab:uploads:check
```

**实例的快照恢复（可选）**
如果从快照恢复，请了解执行此操作的步骤。 此过程超出了 GitLab 支持范围。

## 官方文档参考

<https://docs.gitlab.com/ee/update/plan_your_upgrade.html>

<https://docs.gitlab.com/ee/administration/backup_restore/index.html#restore-gitlab>

<https://docs.gitlab.com/ee/administration/backup_restore/backup_gitlab.html#storing-configuration-files>
