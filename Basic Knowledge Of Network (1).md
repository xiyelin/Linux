## 网络基础知识 (一)

------------------------------------------------

<br>

### OSI（Open System Interconnection，开放系统互连） 七层模型

![OSI_Image](http://hbimg.b0.upaiyun.com/5b0a8c87d7e39d61c631486d3468783161c5f15178d2-AmJgrl_fw658)


	OSI 七层网络模型称为开放式互联参考模型，是逻辑上的定义，一个规范，它将网络从逻辑上分为七层。
	
	目的：解决异种网络互连时所遇到的兼容性问题，帮不同类型的主机实现数据传输。
	
	优点：将服务、接口和协议这三个概念明确地区分开来，七层模型让不同的系统不同的网络之间实现可靠的通讯。

	缺点：虽然体系结构清楚，理论完整，但复杂不实用，所以我们又有了TCP/IP四层模型。


### TCP/IP 四层(或五层)参考模型

![TCP-IP_Image](http://hbimg.b0.upaiyun.com/fadfb70002eb502db28cfce72fc69352a2758cacbe5a-xb6ndJ_fw658)


	TCP/IP协议的开发研制人员将网络分为五个层次，而我们这里将网络接口层和物理层合为主机到网络层。
	
	TCP/IP协议四层的层级结构，每一层呼叫它的下一层所提供的网络来完成自己的需求。分别为：
	
	1.应用层：应用程序间沟通的层；电子邮件传输(SMTP)、文件传输协议(FTP)、网络远程访问协议(Telnet)等。
	
	2.传输层：提供节点间的数据传送服务；如传输控制协议(TCP)、用户数据报协议(UDP)等，TCP和UDP给数据包
	         加入传输数据并把它传输到下一层中，这一层负责传送数据，并且确定数据被送达并接收。
	          
	3.互连网络层：负责提供基本的数据封包传送功能，让每一块数据包都能够达到目的主机(但不检查是否被正确
				 接收)如网际协议(IP)。
	              
	4.网络接口层：对实际的网络媒体的管理，定义如何使用实际网络来传输数据。
	
	

![TCP-IP-Level_Image](http://hbimg.b0.upaiyun.com/d292c2d9b56528160b337dbacee87c8fd549223410d1c-tALvyx_fw658)



### OSI模型到TCP/IP模型的映射

![OSI_TCP-IP_Image](http://hbimg.b0.upaiyun.com/38222151d8183504d9feee54b9e55fb2601133e612127-b9HXrQ_fw658)



















