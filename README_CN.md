## DW (DiamondWisdomChain)：Ethereum DPOS

**DW（DiamondWisdomChain）**在以太坊go-ethereum(V1.9.25)的基础上实现了DPOS共识机制，并且已成功运营，相关获取地址：

 https://github.com/Dwkchain2021/DW.git

若您有对DW更深入的了解，或需要相关合作，可发送邮件至：dwchain2021@gmail.com

## 系统环境及依赖项安装

DW 运行需要GO语言（V1.13或更高版本）和C语言编译环境，安装运行以CentOS 8 示例.

* c语言和cmake基础环境安装：

  >yum update -y && yum install gcc-c++ epel-release nodejs cmake -y

* NTP服务安装：

  > rpm -ivh http://mirrors.wlnmp.com/centos/wlnmp-release-centos.noarch.rpm

  > yum -y install wntp

* GO语言安装：

  > yum -y install golang

  > go version

* 防火墙配置：

  > systemctl restart firewalld

    >firewall-cmd --zone=public --add-port=30303/tcp -–permanent  #系统默认端口
    >
    >firewall-cmd --zone=public --add-port=8545/tcp  -–permanent   #RPC 默认端口 
  >
    >firewall-cmd --zone=public --add-port=123/udp   --permanent   #NTP 服务默认端口
  
    >firewall-cmd --reload

## 客户端DW

DW 可执行文件在目录 /DW/build/bin

| Command | Description                                                  |
| :-----: | ------------------------------------------------------------ |
|   DW    | DW客户端，是DW网络的主要入口，其可以以完整的节点运行。其他进程也可以使用它作为网关，通过HTTP、WebSocket和/或IPC传输之上公开的JSON-RPC端点链接DW网络。 |

## DW运行

DW运行模式及命令与以太坊geth相同，具体信息可参考以太坊geth或邮件咨询：dwchain2021@gmail.com


