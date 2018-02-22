---
title: "新闻热词:从爬虫到react native应用"
date: 2018-02-21
comments: true
categories:  app
tags:
keywords:

---

## 背景
1. 由于只想了解当天新增的top热词，减少过多信息干扰，打算做一款app实现这个功能。
2. 架构： 热词抓取 -> mysql <=> nodejs <=> nginx <=> react native应用  

## 软件安装：
从阿里云申请的CentOS7.4裸机，因此软件安装列表如下：
1. jdk： yum install java-1.7.0-openjdk-devel
2. maven：  wget apache-maven-3.3.9-bin.tar.gz && add to /etc/profile && source  
3. ssh免密登录：scp ~/.ssh/id_rsa.pub root@阿里云服务器ip:~/.ssh/authorized_keys
4. nodejs：  sudo yum -y install npm && sudo npm install -g n && sudo n 9.4.0
5. mysql：  
  wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm  
  rpm -ivh mysql-community-release-el7-5.noarch.rpm  
  yum install mysql-community-server  
  service mysql restart
6. nginx:  
  wget http://dl.Fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm   
  rpm -ivh epel-release-latest-7.noarch.rpm  && yum install nginx -y  
  vim /etc/nginx/conf.d/nginx.yourservice.conf :  
  ```
  server {
      listen   80;
      server_name 你的域名;  #例如到阿里云申请域名，然后在域名解析设置，使用记录类型A
      access_log /var/log/nginx/yourservice-access.log;
      error_log /var/log/nginx/yourservice-error.log;
      location / {
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header Host  $http_host;
          proxy_set_header X-Nginx-Proxy true;
          proxy_set_header Connection "";
          proxy_pass http://127.0.0.1:3000; #nodejs web服务监听的端口
          proxy_redirect default;
      }
      location /static/ {
      }
  }
  ```
  systemctl start nginx.service 启动nginx  
  **注意**：使用阿里云服务器遇到个坑，localhost可以访问http接口，用ip无法访问，误以为是防火墙问题，后来在阿里云－实例安全组修改：允许80地址段访问才解决。


## 爬虫(java):
1. 数据来源: [百度热词榜](http://top.baidu.com/category?c=513&fr=topbuzz_b344_c513)、 [神马热词榜](http://api.m.sm.cn/rest?method=tools.hot&source=home&start=1)、
[搜狗实时热词榜](http://top.sogou.com/hot/shishi_1.html)、[搜狗微信热词榜](http://weixin.sogou.com/)
2. 数据处理: 解析使用jsoup(java的HTML解析器),数据存储使用mysql. [代码](https://github.com/lihonghong/news-app/tree/master/news-app-crawler)
3. crontab定时job: 设置/var/spool/cron/下的配置文件,每15分钟抓取一次热词:   
15 * * * * cd /your path/news-app-crawler/release/bin && sh crawler.hotquery.sh  > crawler.log

## 服务端web(nodejs):
1. 创建node项目，node app.js启动web服务，在浏览器中打开 http://localhost:3000 查看结果。
2. node连接数据库配置见[代码](https://github.com/lihonghong/news-app/blob/master/news-app-web/routes/database.js) 。   
**注意**:
mysql连接有时间限制，当连接超过一定时间没有活动后，会自动关闭该连接，因此需要加上重连机制。另外时区设置为UTC，否则获得的时间有偏差。

## 客户端app(react native):
1. 环境准备可以直接参考facebook的文档 [react-native](https://facebook.github.io/react-native/docs/getting-started.html) ，很详细。主要是ios要确保xcode8以上版本，android确保java8及android 6.0 sdk。  
2. 创建react项目：react-native init AwesomeProject  
3. 运行ios项目：react-native run-ios  
4. 运行android项目：react-native run-android
5. 获取web接口热词并展现，参见[代码](https://github.com/lihonghong/news-app/blob/master/newsAppReact/App.js)
6. 最终热词列表及点击结果如下：  
<img src="/images/png/hotquery.list.png" width="220" />  <img src="/images/png/hotquery.search.png" width="220"/>
