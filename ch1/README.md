# iptables使用简介

1.1 iptables
> 由Netfilter项目开发(http://www.netfilter.org)，自2001年1月Linux2.4内核发布，称为Linux的一部分
> iptables已发展成为一个功能强大的防火墙，具备商业防火墙专有的大多数功能。例如，iptables提供了全面的协议状态跟踪 v、数据包的应用层检查、速率限制和一个功能强大的机制以指定过滤策略
> Netfilter为Linux提供所有包过滤和包修改设施，也就是Linux内核中的一个框架，它可以用于在不同阶段将函数挂接(hook)进网络栈。另一方面iptables使用Netfilter框架旨在将对数据包执行操作（如过滤）的函数挂接进网络栈
    Netfilter提供了一个框架；Iptables在它之上建立了防火墙功能
> iptables还指同名的用户层工具，它解析命令行并将防火墙策略传递给内核

1.2 使用iptables进行包过滤
> iptables策略是由一组有序的规则建立的，它告诉内核应如何处理某些类别的数据包
> 每一个iptables规则应用于一个表中的一个链
> 一个iptables链是一个规则集，这些规则按序与包含共同特征的数据包进行比较


1.2.1 表
> filter: 过滤规则
> nat: NAT规则
> mangle: 用于修改分组数据的特定规则
> raw: 独立于Netfilter连接跟踪子系统起作用的规则

1.2.2 链
> 每个表都有自己的一组内置链，用户还可以对链进行自定义，filter表中：INPUT 、OUTPUT、FORWARD链

- 当一个数据包由内核中的路由计算确定为指向本地Linux系统（即该数据包指向一个本地套接字）之后，它将经过INPUT链检查
- OUTPUT链保留给由Linux系统自身生成的数据包
- FORWARD链管理经过Linux系统路由的数据包（即当iptables防火墙用于连接两个网络，并且两个网络之间的数据包必须流经该防火墙）
- PREROUTING链 用于在内核进行IP路由计算之前修改数据包的头部
- POSTROUTING链 用于在内核进行IP路由计算之后修改数据包的头部

1.2.3 匹配
> 每个iptables规则都包含一组匹配以及一个目标，后者告诉iptables对于符合规则的数据包应该采取什么动作

1.2.4 目标
> iptables支持一组目标，它们用于在数据包匹配一条规则时触发一个动作
- ACCEPT -- 允许数据包通过
- DROP -- 丢弃数据包，不对数据包做进一步的处理，对接收栈而言，就好像该数据包从来没有被接收一样
- LOG -- 将数据包信息记录到syslog
- REJECT -- 丢弃数据包，同时发送适当的响应报文（例如，针对TCP连接的TCP重置数据包或针对UDP数据包的ICMP端口不可达消息）
- RETURN -- 在调用链中继续处理数据包

1.3 安装iptables

