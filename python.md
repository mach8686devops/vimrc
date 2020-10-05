
yum -y install wget && wget -O install.panel.sh http://d.hws.com/linux/master/script/install.panel.sh && bash install.panel.sh


wget -O install.panel.sh http://d.hws.com/linux/master/script/install.panel.sh && sudo bash install.panel.sh





nginx 常见的负载均衡有哪几种：

轮询（默认）
　　轮询是默认的方式，轮询的方法是通过按照时间顺序将请求往不同的后端服务器发送，来缓解服务器的压力。如果后台服务器上某一台宕机了，它可以自动剔除。缺点：可靠性低和负载分配不均衡。适用于图片服务器和静态页面服务器集群。

weight
　　指定轮询几率，weight 和访问比率成正比，用于后端服务器性能不均的情况。
例如： 
upstream bakend { 
　　server 192.168.159.10 weight=10; 
　　server 192.168.159.11 weight=10; 
} 
ip_hash
　　根据每个请求的 ip 的 hash 结果分配，因此每个固定 ip 能访问到同一个后端服务器，可以解决 session 问题。
例如： 
upstream resinserver{ 
　　ip_hash; 
　　server 192.168.159.10:8080; 
　　server 192.168.159.11:8080; 
} 
fair（第三方）
　　按照后端服务器的相应时间来分配请求，时间短的优先分配。

例如：
upstream resinserver{ 
　　server server1; 
　　server server2; 
　　fair; 
} 
url_hash（第三方）
　　按照访问 url 的 hash 结果来分配请求，每个固定的 url 访问同一个后端服务器。如果后端服务器是缓存时效率高。

例如：在upstream中加入hash语句，server语句中不能写入weight等其他的参数，hash_method是使用的hash算法：
upstream resinserver{ 
　　server squid1:3128; 
　　server squid2:3128; 
　　hash $request_uri; 
　　hash_method crc32; 
} 

tips: 
upstream resinserver{　　#定义负载均衡设备的IP及设备状态 
ip_hash; 
server 127.0.0.1:8000 down; 
server 127.0.0.1:8080 weight=2; 
server 127.0.0.1:6801; 
server 127.0.0.1:6802 backup; 
} 
Nginx 不仅仅是一款优秀的负载均衡器/反向代理软件，它同时也是功能强大的 Web 应用服务器，可以做七层的转发 URL 和目录的转发都可以做：

nginx工作在网络的第7层，所以它可以针对http应用本身来做分流策略，比如针对域名、目录结构等
nginx对网络的依赖较小，理论上只要ping得通，网页访问正常，nginx就能连得通
nginx安装和配置比较简单，测试起来也很方便 
nginx可以检测到服务器内部的故障，比如根据服务器处理网页返回的状态码、超时等等，并且会把返回错误的请求重新提交到另一个节点。




工单系统  https://github.com/lanyulei/ferry


集监控点监控、日志监控、数据可视化以及监控告警为一体的国产开源监控系统，直接部署即可使用。

https://gitee.com/xrkmonitorcom/open



https://gitee.com/explore/manage-monitor?lang=Go
