---
title: Hugo博客搭建、部署
date: 2021-09-03T15:00:00+08:00
tags: ['hugo']
slug: 2021090301
draft: false
isCJKLanguage: true
---

年纪大了记性不好，以防忘记，做个记录

## 一、环境配置

- 安装GoLang
  - 下载`msi文件`

  ```bash
  go env #查看得到go的配置信息
  go version #查看go的版本号
  ```

- 安装git
  	[Windows系统Git安装教程（详解Git安装过程）](https://www.cnblogs.com/xueweisuoyong/p/11914045.html)

- 安装hugo
  - 下载适合版本的hugo
  - 打开cmd 
```bash
    cd D:\
    mkdir hugo
    cd hugo
    mkdir bin Sites
    set PATH=%PATH%;D:\hugo\bin
```

  - 使用`set PATH=%PATH%;D:\hugo\bin`失败的话，从控制面板>系统环境变量，进行添加
  - 将*exe文件*解压到D:\Hugo\bin\ ，并重命名为*hugo.exe*

## 二、建立本地站点

```bash
cd D:\hugo\Sites
hugo new site myblog
```

## 三、添加主题

```bash
git init #在站点根目录
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```

**记得把主题内所有关于git的文件删除**，我不知道为什么，留着就没办法push，一直报错

## 四、部署

### 部署到GitHub

[使用Github(Action)+Hugo搭建自己的博客_Redisread的博客-CSDN博客](https://blog.csdn.net/weixin_41263449/article/details/107584336)

1. 创建站点仓库并设置Github Page
   * 仓库名为`username.github.io`
   * 添加一个主题[^1]
   * 设置GitHub Page
2. 创建项目仓库
3. 上传源代码
   ```bash
   #在站点根目录下执行
   git init
   git add .
   git commit -m "first time"
   git remote add origin https://github.com/<username>/<项目仓库名>.git #连接本地与仓库
   git pull origin main #注意Branch名称
   git push -u origin main
   ```
4. 创建ssh-key
   ```bash
   ssh-keygen -t rsa -b 4096 -C "$(git config user.email)" -f gh-pages -N ""
   ```
   * 私钥放在项目仓库
   * 公钥放在站点仓库

---

**大失败**
还是本地build，上传public

### 使用Nginx部署

待尝试



[^1]: 为了能设置GitHub Page





