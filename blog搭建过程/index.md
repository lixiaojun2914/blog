---
title: hexo-indigo+github+nginx博客搭建过程
date: 2019-01-21
categories:
    - 博客搭建
description: 旧博客搭建
slug: 哈哈哈哈
image: pawel-czerwinski-8uZPynIu-rQ-unsplash.jpg
tags:    
    - blog
    - hexo
---
# 安装node.js
```bash
apt-get -y install nodejs
```
# 安装git
```bash
apt-get -y install git
```
# 安装nginx
```bash
apt-get -y install nginx
```
# 安装hexo
```bash
npm install -g hexo-cli
```
# 配置hexo
- 新建hexo项目
```bash
mkdir ~/bash
hexo init ~/bash
cd ~/bash
npm install
```
- 安装indigo主题
```bash
# 下载主题
git clone git@github.com:yscoder/hexo-theme-indigo.git themes/indigo
# 安装相关依赖
npm install hexo-renderer-less --save
npm install hexo-generator-feed --save
npm install hexo-generator-json-content --save
npm install hexo-helper-qrcode --save
# 开启tags页面
hexo new page tags
```
- 配置hexo的_config.yml
以下只列出修改的位置
```yaml
# 设置博客相关信息
title: 夜航的小王子
subtitle: 记录学习的技能和遇到的问题
description: 
keywords:
author: Li Xiaojun
language: zh-Hans
timezone: Asia/Shanghai

# URL
url: http://www.lixiaojun.tk
email: 982090951@qq.com
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

# 主题配置
theme: indigo
feed: 
        type: atom
        path: atom.xml
        limit: 0
jsonContent:
        meta: false
        pages: false
        posts:
                title: true
                date: true
                path: true
                text: true
                raw: false
                content: false
                slug: false
                updated: false
                comments: false
                link: false
                permalink: false
                excerpt: false
                categories: false
                tags: true

# 部署到git
deploy: 
  type: git
  repo: https://github.com/lixiaojun2914/blog.git
```
- 配置themes/indigo目录的_config.yml
以下只列出修改的位置
``` yaml
配置导航栏
menu:
  home:
    text: 主页
    url: /
  archives:
    text: 文章
    url: /archives
  tags:
    text: 标签
    url: /tags
  # th-list:
  #   text: 分类
  #   url: /categories
  github:
    url: https://github.com/lixiaojun2914
    target: _blank
  # weibo:
  #   url: http://www.weibo.com/ysweb
  #   target: _blank
  # link:
  #   text: 管理
  #   url: /admin

# 你的头像url
avatar: /img/avatar.jpg
# avatar link
avatar_link: /
# 头像背景图
brand: /img/brand.jpg
# favicon
favicon: /favicon.ico

# email
email: 982090951@qq.com


# 是否开启打赏，关闭 reward: false
reward: false
  
# 配置valine评论系统
valine:
  enable: true # 如果你想使用valine，请将值设置为 true
  appId:  your appid # your leancloud appId
  appKey:  your appkey # your leancloud appKey
  notify: false # Mail notify
  verify: false # Verify code
  avatar: mm # Gravatar style : mm/identicon/monsterid/wavatar/retro/hide
  placeholder: ヾﾉ≧∀≦)o来啊，快活啊!  # Comment Box placeholder
  guest_info: nick,mail,link # Comment header info
  pageSize: 10 # comment list page size
```
- 配置source/tags/index.md
```
---
title: Tags
date: 2019-01-20 08:19:25
layout: tags
comments: false # 关闭tags的评论
---
```
# 配置/etc/nginx/nginx.conf
```nginx
# user www-data;
user root;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
	worker_connections 768;
	# multi_accept on;
}

http {

	##
	# Basic Settings
	##

	sendfile on;
	tcp_nopush on;
	tcp_nodelay on;
	keepalive_timeout 65;
	types_hash_max_size 2048;
	# server_tokens off;

	# server_names_hash_bucket_size 64;
	# server_name_in_redirect off;

	include /etc/nginx/mime.types;
	default_type application/octet-stream;

	##
	# SSL Settings
	##

	ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE
	ssl_prefer_server_ciphers on;

	##
	# Logging Settings
	##

	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;

	##
	# Gzip Settings
	##

	gzip on;

    # 注释下面两行,否则默认显示nginx导航页
	#include /etc/nginx/conf.d/*.conf;
	#include /etc/nginx/sites-enabled/*;
	server {
		# server_name 127.0.0.1;
		location / {
			root /root/blog/public; # 渲染后的静态页面所在位置
			index index.html; # 启动后显示的主页面
		}
	}
}
```
# 启动nginx服务
```bash 
service nginx start
```
# 新建文章
方法一：使用命令
```bash
hexo new 文章名
```
方法2：
直接在source/_posts内新建一个 文章名.md 文件
# 生成页面并保存
```bash
hexo g -d
```