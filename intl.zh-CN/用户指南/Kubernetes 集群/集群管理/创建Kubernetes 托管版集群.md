# 创建Kubernetes 托管版集群 {#task_skz_qwk_qfb .task}

您可以通过容器服务控制台非常方便的创建Kubernetes托管版集群。

您需要开通容器服务、资源编排（ROS）服务和访问控制（RAM）服务。

登录 [容器服务管理控制台](https://cs.console.aliyun.com/)、[ROS 管理控制台](https://ros.console.aliyun.com/) 和 [RAM 管理控制台](https://ram.console.aliyun.com/) 开通相应的服务。

**说明：** 容器服务 Kubernetes 托管版集群部署依赖阿里云资源编排 ROS 的应用部署能力，所以创建 Kubernetes 托管版集群前，您需要开通 ROS。

-   用户账户需有 100 元的余额并通过实名认证，否则无法创建按量付费的 ECS 实例和负载均衡。
-   随集群一同创建的负载均衡实例只支持按量付费的方式。
-   Kubernetes 集群仅支持专有网络VPC。
-   每个账号默认可以创建的云资源有一定的配额，如果超过配额创建进群会失败。请在创建集群前确认您的配额。如果您需要提高您的配额，请提交工单申请。
    -   每个账号默认最多可以创建 100 个安全组。
    -   每个账号默认最多可以创建 60 个按量付费的负载均衡实例。
    -   每个账号默认最多可以创建 20 个EIP。

1.  登录 [容器服务管理控制台](https://cs.console.aliyun.com/?spm=a2c4g.11186623.2.7.1PrXU7#/overview/all)。 
2.  在 Kubernetes 菜单下， 单击左侧导航栏中的**集群**，进入集群列表页面。单击页面右上角的**创建 Kubernetes 集群**。 
3.  在创建 Kubernetes 集群页面，选择**Kubernetes 托管版（公测）**。 
4.  填写集群的名称。 

    集群名称应包含 1~63 个字符，可包含数字、汉字、英文字符或连字符（-）。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921257_zh-CN.png)

5.  选择集群所在的地域和可用区。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921258_zh-CN.png)

6.  设置集群的网络。 

    **说明：** Kubernetes 集群仅支持专有网络。

    **专有网络**：您可以选择**自动创建**（创建 Kubernetes 集群时，同步创建一个 VPC）或者**使用已有**（使用一个已有的 VPC）。选择**使用已有**后，您可以在已有 VPC 列表中选择所需的 VPC 和交换机。

    -   选择**自动创建**，创建集群时，系统会自动为您的 VPC 创建一个 NAT 网关。
    -   选择**使用已有**，如果您使用的 VPC 中当前已有 NAT 网关，容器服务会使用已有的 NAT 网关；如果 VPC 中没有 NAT 网关，系统会默认自动为您创建一个 NAT 网关。如果您不希望系统自动创建 NAT 网关，可以取消勾选页面下方的**为专有网络配置 SNAT**。

        **说明：** 若选择不自动创建 NAT 网关，您需要自行配置 NAT 网关实现 VPC 安全访问公网环境，或者手动配置 SNAT，否则 VPC 内实例将不能正常访问公网，会导致集群创建失败。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921259_zh-CN.png)

7.  设置节点类型。 

    **说明：** 支持创建**按量付费**和**包年包月**两种节点类型。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921260_zh-CN.png)

8.  设置实例。 

    **说明：** 

    -   目前仅支持 CentOS 操作系统。
    -   每个集群最少包含 2 个节点。
    -   每个集群最多可包含 48 个节点。如果您需要创建更多的节点，请提交工单申请。
    -   默认为实例挂载系统盘，支持高效云盘和SSD云盘。
    -   支持为实例挂载 1 个数据盘，支持高效云盘和SSD云盘。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921261_zh-CN.png)

9.  设置登录方式。 

    -   设置密钥。

        您需要在创建集群的时候选择密钥对登录方式，单击**新建密钥对**，跳转到ECS云服务器控制台，创建密钥对，参见[创建 SSH 密钥对](../../../../intl.zh-CN/用户指南/密钥对/创建 SSH 密钥对.md#)。密钥对创建完毕后，设置该密钥对作为登录集群的凭据。

    -   设置密码。
        -   **登录密码**：设置节点的登录密码。
        -   **确认密码**：确认设置的节点登录密码。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921262_zh-CN.png)

10. 设置**Pod 网络 CIDR** 和**Service CIDR** 

    **说明：** 

    -   该选项仅在设置专有网络选择**使用已有**VPC时出现。
    -   **Pod 网络 CIDR**和**Service CIDR**两者都不能与 VPC 及 VPC 内已有 Kubernetes 集群使用的网段重复，创建成功后不能修改。且 Service 地址段也不能和 Pod 地址段重复，有关 Kubernetes 网络地址段规划的信息，请参考[VPC下 Kubernetes 的网络地址段规划](intl.zh-CN/用户指南/Kubernetes 集群/集群管理/VPC下 Kubernetes 的网络地址段规划.md#)。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921265_zh-CN.png)

11. 设置是否为专有网络配置 SNAT 网关。 

    **说明：** 

    -   若您选择**自动创建** VPC 时必须配置 SNAT；
    -   若您选择**使用已有**VPC，可选择是否自动配置SNAT网关。若选择不自动配置 SNAT，您可自行配置NAT 网关实现 VPC 安全访问公网环境；或者手动配置 SNAT，否则 VPC 内实例将不能正常访问公网，会导致集群创建失败。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921267_zh-CN.png)

12. 设置是否启用云监控插件。 您可以选择在 ECS 节点上安装云监控插件，从而在云监控控制台查看所创建 ECS 实例的监控信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921268_zh-CN.png)

13. 设置启用的网络插件，支持Flannel和Terway网络插件。 

    -   Flannel：简单稳定的社区的Flannel 插件。
    -   Terway：阿里云容器服务自研的网络插件，支持将阿里云的弹性网卡分配给容器，支持Kubernetes的NetworkPolicy来定义容器间的访问策略，支持对单个容器做带宽的限流，目前处于公测阶段。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921269_zh-CN.png)

14. 设置RDS白名单。 

    将节点 IP 添加到 RDS 实例的白名单。

    **说明：** 该选项仅在设置专有网络选择**使用已有**VPC时出现。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106094921270_zh-CN.png)

15. 单击**创建集群**，启动部署。 

    **说明：** 一个包含多节点的 Kubernetes 集群的创建时间一般约为 5 分钟。


集群创建成功后，您可以在容器服务管理控制台的 Kubernetes 集群列表页面查看所创建的集群。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106095021425_zh-CN.png)

您可以单击操作列的**查看日志**，进入集群日志信息页面查看集群的日志信息。 您也可以在集群日志信息页面中，单击**资源栈事件**查看更详细的信息。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106095021426_zh-CN.png)

在集群列表页面中，找到刚创建的集群，单击操作列中的**管理**，查看集群的基本信息和连接信息。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106095021427_zh-CN.png)

**其中：**

-   **API Server 公网连接端点**：Kubernetes 的 API Server 对公网提供服务的地址和端口，可以通过此服务在用户终端使用 kubectl 等工具管理集群。
-   **服务访问域名**：为集群中的服务提供测试用的访问域名。服务访问域名后缀是`<cluster_id>.<region_id>.alicontainer.com`。

您可以[通过 kubectl 连接 Kubernetes 集群](intl.zh-CN/用户指南/Kubernetes 集群/集群管理/通过 kubectl 连接 Kubernetes 集群.md#)，执行`kubectl get node`查看集群的节点信息。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40726/154106095021438_zh-CN.png)

