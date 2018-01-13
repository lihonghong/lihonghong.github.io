---
title: "octopress && github 建个人博客"
excerpt: "octopress"
date: 2016-01-28 20:19:35 +0800
comments: true
keywords: octopress

---

### ubuntu 14.04:
##### Step 1 注册github
   > 以用户名.github.io格式创建个博客项目

##### Step 2 安装ruby
   > sudo apt-get install ruby ruby-dev

<!-- more -->

##### Step 3 安装octopress

*  获取：

  > git clone git://github.com/imathis/octopress.git octopress

  > cd octopress

  > ruby --version

*  安装依赖：

  > gem install bundler

  > bundle install

*  安装默认主题:

  > rake install  

##### Step 4 项目配置

  > rake setup_github_pages  

##### Step 5 写博客

* 切换到源码分支：git checkout source

* 新建一篇博客
  > rake new_post[title]
* 本地预览  
  > rake preview

##### Step 6 发布博客

  生成及部署：
  > rake generate  
  rake deploy


### mac 10.11.2 (EI CAPITAN):

##### 遇到安装报错及解决
>An error occurred while installing RedCloth (4.2.9), and Bundler cannot continue.Make sure that `gem install RedCloth -v '4.2.9'` succeeds before bundling.

1. Clear git cache
rm -rf /usr/local/.git

2. Update Homebrew
brew update

3. Install rvm
curl -L https://get.rvm.io | bash -s stable --ruby

4. Install ruby 2.2.3

   rvm install ruby-2.2.3

   rvm use 2.2.3  && add in  ~/.bash_profile
   我在添加到~/.zshrc遇如下错误：RVM is not a function, selecting rubies with 'rvm use ...' will not work.

   rvm rubygems latest

6. Install Octopress's dependencies:
gem install bundler
bundle install

7. See if your octopress works:
rake preview

### 如果需要绑定到自己域名
在域名商那添加cname记录到xxx.github.io
在github项目setting设置域名

### 增加统计工具
到https://web.umeng.com 申请，然后拷贝代码到source/_includes/custom/footer.html中，重新部署即可。

### 搜索优化
生成的文章添加tags、keywords、description字段

### rake gen_deploy失败： ! [rejected]  master -> master (non-fast-forward)
cd octopress/_deploy
git pull origin master
cd ..
rake deploy

### 添加评论
注册disqus，拿到disqus_short_name添加到config.yml, 注意url应和注册时提交的一致，最后不要加/

### 投放google adsense
首先在/source/includes/asdies/advertise.html添加谷歌广告平台注册的代码，然后到config.yml的default_asides添加asides/advertise.html。

### 参考：
让Octopress在多台电脑工作：http://foggry.com/blog/2014/04/02/ru-he-pei-zhi-rang-ni-de-octopressbo-ke-zai-duo-tai-macshang-tong-shi-shi-yong/

解决跨机器分支冲突：http://weishi.github.io/blog/2013/07/24/setup-an-existing-octopress-repository-after-git-clone/

mac冲突解决：http://soledad.me/blog/2015/12/21/octopress-and-el-capitan/

自定义功能：http://foggry.com/blog/2014/04/28/custom-your-octopress-blog/
