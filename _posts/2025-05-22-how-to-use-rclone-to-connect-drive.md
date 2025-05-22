---
title: "使用Rclone工具连接Google Drive"
date: 2025-05-22
excerpt: "Rclone 连接 Google Drive 完全指南：记录了我使用rclone连接Google Drive的过程，这样就可以在Remote科研的时候使用Google Drive下载远在国外的服务器上的大文件了"
layout: post

---
# 【保姆级教程】我是如何使用 Rclone 连接并并上传文件到 Google Drive 的
这也是我在Remote科研中的一些探索，由于某些需求，我需要从服务器中下载一些大型的文件，但是在国内连接国外服务器的时候，用SSH连接都十分的不稳定，即便使用SFTP传输文件速度也只有几十KB每秒。

我发现在科学上网的时候，直接从Google Drive中下载文件的速度就很快了，即便这比较耗费流量，但是也值得了，毕竟节省了时间。接下来是我配置的过程，有一些地方可能会有遗漏，可以留言告诉我。

由于我在服务器上的权限并不多，因此不能使用`sudo`，所以另辟蹊径。
```bash
curl -O https://downloads.rclone.org/rclone-current-linux-amd64.zip
unzip rclone-current-linux-amd64.zip
cd rclone-*-linux-amd64

mkdir -p ~/.local/bin
cp rclone ~/.local/bin/

echo 'export PATH=$HOME/.local/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```
这样即便权限不是很高，也可以在命令行中使用rclone命令了，无需sudo。

运行一下命令行启动配置流程
```bash
rclone config
```
就开始配置了，前面的配置都比较简单，设置名称，选择云硬盘的类型，这里我选择的是drive，中间需要输入一个Client ID以及Client Secret，会弹出来一个网址https://rclone.org/drive/#making-your-own-client-id 告诉你如何配置最后获得所需要的Client ID以及Client Secret，前面的步骤较为简单，我在下面会贴出我在配置过程中比较困难的截图：
其中第5步，需要add some scopes，这一步我找了很久，步骤如下：![寻找Credentials](/assets/images/blog/5-22-1.png) ![寻找OAuth](/assets/images/blog/5-22-2.png) ![寻找scope添加按钮](/assets/images/blog/5-22-3.png)然后就可以按照网站上的指示添加列出来的几个网址了。

将得到的client ID and client secret复制到rclone中即可，接下来会遇到![4](/assets/images/blog/5-22-4.png)这一步是设置访问权限，如果你希望能够读写所有文件，上传或者下载文件就可以选择第1个。

接下来的配置只要选择default选项就可以了。

然后在这一步![授权](/assets/images/blog/5-22-5.png)就需要借助本地的电脑进行Google Drive授权了，在本地下载好rclone（如果是win，可以在[这里](https://rclone.org/downloads/)选择合适的版本进行下载）之后，复制那段`rclone authorize ...`，本地的电脑就会弹出来浏览器，接着授权就可以了。

！！需要注意的是，如果你在科学上网，记得设置好代理端口，比如我在过程中遇到一个问题：当我授权完成之后，没有弹出来对应的token，报错原因是` NOTICE: Fatal error: failed to get token: Post "https://oauth2.googleapis.com/token": proxyconnect tcp: dial tcp 127.0.0.1:7890: connectex: No connection could be made because the target machine actively refused it.`这里就需要将代理的端口设置为7890，完成之后重新开始代理，重复前面的授权步骤，就可以在终端中得到token，完整的复制到服务器的终端中的config token中，就算**完成了配置**。
![完成配置](/assets/images/blog/5-22-6.png)

接下来就可以通过：
```bash
rclone copy file_path gyr:

rclone copy file_path gyr:Backup/
```
将文件上传到Drive云盘中了。


    

