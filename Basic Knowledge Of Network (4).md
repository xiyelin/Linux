## IP地址与路由

	IPv4的IP地址长度为4字节,通常采用点分十进制表示法；例如0xc0a80002表示为192.168.0.2。 Internet被各种路由器和网关
	设备分隔成很多网段,为了标识不同的网段,需要把32位的IP地址划分成网络号和主机号两部分,网络号相同的各主机位于同一网
	段,相互间可以直接通信,网络号不同的主机之间通信则需要通过路由器转发。
	
------------------------------------------------------------


## IP地址

	曾经提出一种划分网络号和主机号的方案,把所有IP地址分为以下五类：
	
![image](http://hbimg.b0.upaiyun.com/74eda50e7a424af2924ba3c9722c5de63d247e341b544-jm3xPI_fw658)

	缺点：

	这种划分方案的局限性很快显现出来,大多数组织都申请B类网络地址, 导致B类地址很快就分配完了,而A类却浪费了大量地址。这种
	方式对网络的划分是flat的而不是层级结构(hierarchical)的,Internet上的每个路由器都必须掌握所有网络的信息,随着大量C类网
	络的出现,路由器需要检索的路由表越来越庞大,负担越来越重。
	
<br>
<br>

	新的划分方案CIDR(Classless Interdomain Routing)：
	
	网络号和主机号的划分需要用一个额外的子网掩码(subnet mask)来表示,而不能由IP地址本身的数值决定,也就是说,网络号和主机号
	的划分与这个IP地址是A类、 B类还是C类无关,因此称为Classless的。这样,多个子网就可以汇总(summarize)成一个Internet上的网络。

	IP地址与子网掩码做与运算可以得到网络号,主机号从全0到全1就是子网的地址范围。
	
![image](http://hbimg.b0.upaiyun.com/601d59da0bd138768ba217ae66cc90cc1a940ed326554-9FUjOK_fw658)

<br>
	IP地址和子网掩码还有一种更简洁的表示方法,例如140.252.20.68/24,表示IP地址为140.252.20.68, 子网掩码的高24位是1,也就是
	255.255.255.0。
	
<br>

	组建局域网（私有IP地址）：
	
	如果一个组织内部组建局域网,IP地址只用于局域网内的通信,而不直接连到Internet上,理论上使用任意的IP地址都可以,但是RFC 1918
	规定了用于组建局域网的私有IP地址,这些地址不会出现在Internet上,如下所示。
	
	10.*,前8位是网络号,共16,777,216个地址；
	172.16.* 到 172.31.*,前12位是网络号,共1,048,576个地址；
	192.168.*,前16位是网络号,共65,536个地址；
	
	使用私有IP地址的局域网主机虽然没有Internet的IP地址,但也可以通过代理服务器或NAT(网络地址转换)等技术连到Internet上。

<br>

	几种特殊的IP地址：
	
	1.环回测试：
	  127.*的IP地址用于本机环回(loop back)测试,通常是127.0.0.1。 loopback是系统中一种特殊的网络设备,如果发送数据包的目
	  的地址是环回地址,或者与本机其它网络设备的IP地址相同,则数据包不会发送到网络介质上,而是通过环回设备再发回给上层协
	  议和应用程序,主要用于测试。
	
![image](http://hbimg.b0.upaiyun.com/2b4c695c4f9607670f8035c478eadda30168d8a916824-au2AgN_fw658)

<br>

	
	
	
	
	
	
	
	
	
	
	
	
	




























	
	
	
	