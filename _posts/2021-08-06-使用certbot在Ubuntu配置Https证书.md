---
layout: post
title:  "使用certbot在Ubuntu配置Https证书"
date:   2021-08-06 12:30:00 +0800
categories: ubuntu certbot apache
tags:
    - ubuntu
    - certbot
    - apache
---


# 使用certbot在Ubuntu配置Https证书

![image](https://certbot.eff.org/images/certbot-logo-1A.svg)

> 通过Certbot可以轻松配置Https://，[Certbot官网](https://certbot.eff.org/)

## 选择操作系统版本与服务器软件
> 以Apache和Ubuntu 18.04为例

### 1.在服务器上运行SSH
以具有 ```sudo``` 权限的用户身份通过 ```SSH``` 连接到运行你的 ```HTTP``` 网站的服务器。
### 2.安装Snapd
您需要安装 ```snapd``` 并确保按照任何说明启用经典 ```snap``` 支持。
  按照 ```snapcraft``` 网站上的这些说明安装 ```snapd```。

[点击安装snapd](https://snapcraft.io/docs/installing-snapd/)
### 3.确保你的Snapd 版本是最新的
在机器上的命令行执行以下说明，确保你拥有最新版本的```snapd```。

```
$ sudo snap install core; sudo snap refresh core
```
### 4.删除 certbot-auto 和任何 Certbot OS 包
如果您使用```apt```、```dnf``` 或 ```yum``` 等操作系统软件包管理器安装了任何```Certbot```软件包，则应在安装```Certbot snap```之前将其删除，以确保在运行命令 ```certbot``` 时使用的是 ```snap```，而不是从您的操作系统软件包安装 经理。 执行此操作的确切命令取决于您的操作系统，但常见示例是 ```sudo apt-get remove certbot```、```sudo dnf remove certbot``` 或 ```sudo yum remove certbot```。

如果您之前通过 ```certbot-auto``` 脚本使用过 ```Certbot```，您还应该按照 [此处](https://certbot.eff.org/docs/uninstall.html) 的说明删除其安装。

### 5. 安装Certbot
在机器上的命令行上运行此命令以安装 ```Certbot```。

```
$ sudo snap install --classic certbot
```

### 6.准备 Certbot 命令
在机器上的命令行执行以下指令，确保```certbot```命令可以运行。

```
$ sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
### 7.选择您希望如何运行 Certbot 
- 获取并安装您的证书

运行此命令以获取证书并让 ```Certbot``` 自动编辑您的 ```Apache``` 配置以提供服务，只需一步即可打开 ```HTTPS``` 访问。
```
$ sudo certbot --apache
```
- 或者只获取一个证书
如果你感觉更保守，并希望手动更改 ```Apache``` 配置，请运行此命令。
```
$ sudo certbot certonly --apache
```
### 8.测试自动续订
你系统上的 ```Certbot``` 软件包带有一个 ```cron``` 或系统计时器，它们会在你的证书到期之前自动更新证书。 除非你更改配置，否则无需再次运行 ```Certbot```。

你可以通过运行以下命令来测试证书的自动续订：

```
$ sudo certbot renew --dry-run
```
如果该命令正确完成，您的证书将在后台自动更新。
### 9. 确认 Certbot 工作
要确认你的站点设置正确，在浏览器中访问 ``` https://yourwebsite.com/``` 并在 URL 栏中查找锁定图标。

### 总结命令
```
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update

sudo apt-get install certbot python3-certbot-apache

sudo certbot --apache
```

