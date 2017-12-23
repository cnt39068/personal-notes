# Openstack

## OpenStack设计与实现
OpenStack七个核心组件
* Compute
* Object Storage
* Identity
* Dashboard
* Block Storage
* Network
* Image Service

## Training

NFV: Network-function vritualization

Cloud Native application 超级计算: 多台主机合并成一台主机

RabiitMQ: OpenStack消息队列

OpenStack自动安装部署软件
* Devstack: Git源代码安装? 开发者使用。
* RDO
* Fuel

云管理平台/云操作系统
* OpenStack
* CloudStack

四种网络/四种节点
* 控制节点：控制逻辑
* 计算节点：规模，计算节点的数量。虚拟机？
* 网络节点：跨网段的虚拟机的网络交换
* 存储节点
 
OpenStack Shared Services
* Compute
* Networking
* Storage

All-in-one installation: 一个服务器扮演四个角色（四个节点）

Training环境网络设置
* VNet2: 管理网络  192.168.201.0
* VNet3: 计算和网络节点  192.168.192.0
* VNet4: 网络节点对外访问 192.168.11.0
* 没有设置存储结点网络

Linux commands
* service --status-all
  * Apache2
  * ntp
  * glance-api
  * glance-registry
  * rabbitMQ
* source adminrc
* source installrc
* source ….

OpenStack存储服务
* 块存储 Cindar
  * 源自Nova-Volumn
  * OpenStack Block Storage
    * 块存储服务，又称为卷服务Volumn
  * Cindar模块
    * Cinder-volumn：装在哪里根据volumn-provider来决定
* 镜像存储

OpenStack Projects
* Ceilometer: 计量工作居多，monitor不大准确

Keystone
* keystone service-list

Linux虚拟机
* Virt-manager
