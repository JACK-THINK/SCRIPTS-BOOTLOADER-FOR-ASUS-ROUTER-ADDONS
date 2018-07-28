# Readme for ddns

## 概述

1. 本插件用于启动和结束ddns
2. 该插件仅适用于使用HE.NET作为DNS服务提供商的域名
3. 安装本插件后，可直接实现DDNS，不依赖华硕路由器固件中DDNS客户端
4. 当路由器通过PPPoE方式拨号上网时，若获得的IP地址为私有IP，则自动禁用DDNS服务，并向指定邮箱发送提醒邮件

## 安装前提

1. 必须安装并启用entware和monit

## 文件结构

`ASUS_ROUTER/script_bootloader/usr/ddns/`

| 权限      | 名称      | 属性     | 说明             |
| --------- | --------- | -------- | ---------------- |
| rwxrwxrwx | README.md | 普通文件 | 说明文件         |
| rwxrwxrwx | bin       | 目录     | 可执行文件目录   |
| rwxrwxrwx | tmp       | 目录     | 临时文件目录   |
| rwxrwxrwx | usr       | 目录     | 外部软件资源目录 |

`ASUS_ROUTER/script_bootloader/usr/ddns/bin/`

| 权限      | 名称                 | 属性     | 说明                                                         |
| --------- | -------------------- | -------- | ------------------------------------------------------------ |
| rwxrwxrwx | ddns_home_china_enable.service     | 普通文件 | 更新DDNS记录或发送邮件主程序         |
| rwxrwxrwx | ddns_home_china_disable.service    | 普通文件 | 更新DDNS记录为无效地址并停止DDNS服务 |

`ASUS_ROUTER/script_bootloader/usr/ddns/tmp/`

| 权限      | 名称         | 属性     | 说明         |
| --------- | ------------ | -------- | ------------ |
| rwxrwxrwx | mail.tmp | 普通文件 | 使用curl发送邮件时自动生成 |

`ASUS_ROUTER/script_bootloader/usr/ddns/usr/`

| 权限      | 名称         | 属性     | 说明         |
| --------- | ------------ | -------- | ------------ |
| rwxrwxrwx | NO_PUBLIC_IP_ADDRESS | 普通文件 | 通知邮件文件（用于无公网IP时） |

## 安装方法

无需安装

## 调用方法

| 插件文件                   | 插件调用者              |
| -------------------------- | -----------------       |
| ddns_enable.service  | monit.d/ddns_home_china |
| ddns_disable.service | monit.d/ddns_home_china |

## 需修改部分

`ddns/bin/ddns_home_china_enable.service`

| 行号 | 代码                         | 说明                   |
| ---- | ---------------------------- | ---------------------- |
| 26   | `DDNS_HOSTNAME=""`           | 你的域名               |
| 30   | `DDNS_PASSWORD=""`           | 域名更新密码           |
| 34   | `MAIL_SMTP_SERVER="smtp://"` | 发件人的SMTP服务器地址 |
| 38   | `MAIL_PASSWORD=""`           | 发件人密码             |
| 42   | `MAIL_FROM=""`               | 发件人邮箱地址         |
| 46   | `MAIL_TO=""`                 | 收件人邮箱地址         |

`ddns/bin/ddns_home_china_disable.service`

| 行号 | 代码                         | 说明                   |
| ---- | ---------------------------- | ---------------------- |
| 10   | `DDNS_HOSTNAME=""`           | 你的域名               |
| 14   | `DDNS_PASSWORD=""`           | 域名更新密码           |