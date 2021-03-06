
1.安装nginx

yum -y install nginx

如果上一步不行，先安装下面的rpm

rpm -ivh http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm

再执行yum -y install nginx

等待自动安装即可

备注：安装有很多种方式，其他方式请自行搜索

2.启动/停止nginx

启动：service nginx start

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard1.png)

停止：service nginx stop

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard2.png)

重启：service nginx restart

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard3.png)

每次执行命令后，如果都提示OK，那就一切安好了

3.访问nginx服务
(以小编机器为例)

http://192.168.200.140 

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard4.png)

什么情况？？？？？服务启动提示OK啊。。。。。。

我们来检查一下服务是否启动

ps -ef|grep nginx

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard5.png)

服务是正常启动了，没有启动是下面这个样子的：

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard6.png)

而且服务没有启动情况下页面长下面这个样子：

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard7.png)

所以可以排除服务启动出现问题

冷静分析一下，403这不是服务器返回的错误吗？服务器都能应答了！！！！！套路太深了。

还好小编知道点http协议，要不然彻底懵逼了。看来前端同学了解http协议很有必要啊！

现在问题是禁止访问了，对，禁止访问！！！！

掐指一算，估计是iptables（防火墙）或者selinux（安全增强式Linux）的问题
先检查防火墙

service iptables status

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard8.png)

显示not running，说明防火墙是关闭的

再检查下selinux

/usr/sbin/sestatus -v

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard9.png)

current mode 是什么？当前模式，并且还是强制，问题的根源就在这里。

不知道selinux是什么不重要，重要的是我可以关闭你！

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard10.png)

编辑文件，后保存

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard11.png)

重启一下linux

reboot

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard12.png)

休息片刻，连接上linux，检查selinux

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard13.png)

总算是关闭了！！！！扫清障碍，go！！

启动nginx，访问服务

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard14.png)

到这里，服务安装完毕，也可以正常运行了。
