1.解读nginx配置文件nginx.config，

配置文件路径：/etc/nginx

查看nginx.conf

cat nginx.conf

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard15.png)

nginx日志文件，记录服务器访问日志

include /etc/nginx/conf.d/*.conf

上面这一行堪称核武器，流弊闪闪，他可以实现多站点，虚拟主机！！！！

进入到配置文件路径下

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard16.png)

默认情况下，有一个default.conf，

查看一下他是什么

cat default.conf 

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard17.png)

端口和域名：

listen：端口，你可以随意写，但是不要和其他服务的端口冲突

server_name：域名，当然，你也可以写ip

location / {
root  /server/html;
index  index.html;
}

访问http://server_name:listen的时候，nginx服务定位到的路径（root）和文件（index）;

配置文件的关键点解读完毕，那么他怎么实现多站点呢？

复制一个default.conf，什么？？？？？？？

你没有看错，就是复制一下，改名，改端口、域名/ip，就是这么简单！！！

来看看我们的测试服务器配置吧

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard18.png)

h.conf：

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard19.png)

image.conf

![image](https://github.com/INKGROUP/share/blob/master/resources/201705/images/clipboard20.png)

看到这里，你是不是顿悟了？

一个nginx服务下，就这样搞出了多个方式来访问资源，

小编是用来做二级域名使用，区分不同静态资源，提高并发使用的。

至于你想干啥，那就干啥吧！

记住，修改配置文件后，要重启nginx服务才可以生效。



我想对你说：看到这里，已经基本可以满足你学习，开发，测试使用了。但是你要相信，nginx是一个怪兽，还有很多很多流弊的功能等待你探索，本文只是基础的基础。
