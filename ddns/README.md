# Readme for ddns

## 概述

1. 本插件用于安装、配置、启动和结束ddns
2. 该插件仅适用于使用HE.NET作为DNS服务提供商的域名
3. 安装本插件后，可直接实现DDNS，不依赖华硕路由器固件中DDNS客户端
4. 当路由器通过PPPoE方式拨号上网时，若获得的IP地址为私有IP，则自动禁用DDNS服务，并向指定邮箱发送提醒邮件

## 安装前提

1. 必须安装并启用entware和mailx（使用curl发送邮件时无需mailx）

## 文件结构

`ASUS_ROUTER/script_bootloader/usr/ddns/`

| 权限      | 名称      | 属性     | 说明             |
| --------- | --------- | -------- | ---------------- |
| rwxrwxrwx | README.md | 普通文件 | 说明文件         |
| rwxrwxrwx | bin       | 目录     | 可执行文件目录   |
| rwxrwxrwx | tmp       | 目录     | 临时文件目录   |
| rwxrwxrwx | usr       | 目录     | 外部软件资源目录 |

`ASUS_ROUTER/script_bootloader/usr/ddns/bin/`

| 权限      | 名称                 | 属性     | 说明                                       |
| --------- | -------------------- | -------- | ------------------------------------------ |
| rwxrwxrwx | ddns_install         | 普通文件 | 插件的安装程序                             |
| rwxrwxrwx | ddns_enable.service  | 普通文件 | 插件的可执行程序，用于启动程序             |
| rwxrwxrwx | ddns_disable.service | 普通文件 | 插件的可执行程序，用于结束程序             |
| rwxrwxrwx | home_china_curl      | 普通文件 | 更新DDNS记录或发送邮件主程序（使用`curl`） |

`ASUS_ROUTER/script_bootloader/usr/ddns/tmp/`

| 权限      | 名称         | 属性     | 说明         |
| --------- | ------------ | -------- | ------------ |
| rwxrwxrwx | mail.tmp | 普通文件 | 使用curl发送邮件时自动生成 |

`ASUS_ROUTER/script_bootloader/usr/ddns/usr/`

| 权限      | 名称         | 属性     | 说明         |
| --------- | ------------ | -------- | ------------ |
| rwxrwxrwx | NO_PUBLIC_IP_ADDRESS | 普通文件 | 通知邮件文件（用于无公网IP时） |

## 安装方法

执行`/tmp/mnt/ASUS_ROUTER/script_bootloader/usr/ddns/bin/ddns_install`

   > [受支持的路由器型号](https://github.com/Entware/Entware/wiki/Install-on-Asus-stock-firmware)：
   > 
   > | 架构        | 路由器型号                                                   |
   > | ----------- | ------------------------------------------------------------ |
   > | **aarch64** | RT-AC86U                                                     |
   > | **armv7**   | RT-AC68U, RT-AC56U, RT-AC87U, RT-AC3200, RT-AC88U, RT-AC3100, RT-AC5300, GT-AC5300 |
   > | **mipsel**  | RT-N66U, RT-AC66U, RT-N16                                    |

## 调用方法

| 插件文件                          | 插件调用者                   | 调用位置  |
| --------------------------------- | ---------------------------- | --------- |
| ddns_enable.service | list_of_user_custom_scripts | 第61行（安装后需手动配置开机加载。启用：删除行首`#`；禁用：恢复行首`#`） |
| ddns_disable.service | script_bootloader_usb_umount | 自动调用 |

## 需修改部分

`ddns/bin/home_china_curl`

| 行号 | 代码                         | 说明                   |
| ---- | ---------------------------- | ---------------------- |
| 30   | `DDNS_HOSTNAME=""`           | 你的域名               |
| 34   | `DDNS_PASSWORD=""`           | 域名更新密码           |
| 38   | `MAIL_SMTP_SERVER="smtp://"` | 发件人的SMTP服务器地址 |
| 42   | `MAIL_PASSWORD=""`           | 发件人密码             |
| 46   | `MAIL_FROM=""`               | 发件人邮箱地址         |
| 50   | `MAIL_TO=""`                 | 收件人邮箱地址         |