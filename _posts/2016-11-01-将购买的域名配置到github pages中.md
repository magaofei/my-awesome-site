---
layout: post
title: 将购买的域名配置到github pages中

tags: 
- github
comments: true
---

参考 : https://help.github.com/articles/setting-up-an-apex-domain/

1. 在yourname.github.io的Setting中添加你的自定义域名

2. 在域名解析中添加相应的DNS

   > 103.245.222.133


![]({{ site.url }}/assets/"域名解析".png)



## Github pages设置301重定向

购买了域名之后，我们想要让不带www的网址重定向到带www前缀的网址上面

1. 在`yourname.github.io`目录下新建CNAME文件，内容是你的自定义域名比如www.magaofei.com
2. 在域名解析那里，添加CNAME类型的记录，值为`yourname.github.io`



#### [macOS下查看端口和杀掉端口](http://stackoverflow.com/questions/12397175/how-do-i-close-an-open-port-from-the-terminal-on-the-mac)

1. Find out the process ID (PID) which is occupying the port number (e.g., 5955) you would like to free

   ```
   sudo lsof -i :5955
   ```

2. Kill the process which is currently using the port using its PID

   ```
   sudo kill -9 PID
   ```

## 