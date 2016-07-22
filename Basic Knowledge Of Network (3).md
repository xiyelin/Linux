## 网络基础知识（三）

-----------------------------------------------

### 以太网(RFC 894)帧格式

![image](http://hbimg.b0.upaiyun.com/f3a5336c2e39dd2e0fa41356c878b40987f6c2ac173e1-DtPzeb_fw658)


	以太网帧中的数据长度规定最小46字节,最大1500字节,ARP和RARP数据包的长度不够46字节,要在后面补填充位(PAD)。
	
	MTU(最大传输单元)：1500称为以太网的最大传输单元，MTU这个概念指数据帧中有效载荷的最大长度,不包括帧首部的长度。
	
	不同的网络类型有不同的MTU,如果一个数据包从以太网路由到拨号链路上,数据包长度大于拨号链路的MTU了,则需要对数据
	包进行分片(fragmentation)。分片在MAC帧上层完成的。

<br>
<br>

### ARP数据报格式