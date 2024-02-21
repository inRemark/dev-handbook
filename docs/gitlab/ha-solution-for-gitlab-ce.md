# HA Solution Of GitLab CE


## 高可用关键点

**存储高可用**
PostgreSQL高可用
Redis&Sentinel高可用
Gitaly&Praefect多节点

**应用高可用**
GitLab Rails多节点
Sidekiq 多节点

**接入网管高可用**
SLB


## 官方系统架构图

![GitLab系统架构](https://docs.gitlab.com/ee/development/img/architecture_simplified_v14_9.png)

## 官方高可用架构

![GitLab高可用架构图](https://plantuml.gitlab-static.net/png/U9nzLijk6Z4KtVihhCnkMW8DA2IRA0L2L2bgQLYs21d6W8kngUrHWwh-U_qQpyDkLp3ttCUvnxvtvb4g95Hved1u1F98s1a9T8AKCAmkPmovK0SEm1Q90bxb-TERme8X2byuAk04KSIsMEJv5KGIOhg1sIswt-1n2FZ4_XD0JC3zS3oOJG1GV8_L0Glu6q2uvPJYhIASIPFbcQWNj86lY52Pv_1jQCFtH55jpOOtqzdm9evQaW8VoKyJCB81qXbWjjlT5SK7yATRrPDU27uorbB2T_1Pe1rYo5C-SKOK5p0Rp-VpsIWkEjM_9Qr9RkqppF3OA6DAkYgw9KGlS4fBgHMg-j6czTQPKZei1C8x_LodFtiBpERpk-bWaDHEPssfPWet_4FNFjM2IxKNUFdr9S_pxwpV_ymPtA6IgfxY50l4LB_Vghu-kn0PqkgyWLhlcxUkUW--V1f-Y1FMWisGGXiaiIrS-8UaICyJNhfR5bJQRvm9PgEdZ_heccqtkeNz_aAG4nANga5FOtrsvcPyfsexpHBhWozi8lXsqyubAonaCt84YbeFPpPoTGaOpowdwn3ma2XIA_YA2o8j5M7-fRIpBhLkrc_DUE5EzdOu6jjqb9TMko-R7-O4bteYq1xx4U7Mk9RE2BDV1w8m06OxwDRSVl0tGOzls_wUwI1sNFKqxaSD03_dsibDUjD9hv08NmaDj5d4FhsU2RSDLk1r1wmkMHry84M1sQf1BW6vYGUWsZQwfjitNTwHGufuxDHaNg7N7JHGhyDZxYci8a_SgRZbR1ctjrF28THqK9KpS6sPoxfMP0y7xtUdRivjJulwQvF4V4SnA1ff8x39FGLsEk-wD8_LTGggjuJsSU-99lCqM56FqI1K33MP9z4EzSWdvfwgRoxhFqDB4wk76817p0hz9G7-0k8PguG0)


## GitLab组件介绍

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