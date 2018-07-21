# Readme for shadowsocks

## 概述

1. 本插件用于安装、配置、启动和结束shadowsocks
2. ss_local客户端，用来连接远端shadowsocks服务器

## 安装前提

1. 必须安装并启用entware

## 文件结构

`ASUS_ROUTER/script_bootloader/usr/shadowsocks/`

| 权限      | 名称      | 属性     | 说明           |
| --------- | --------- | -------- | -------------- |
| rwxrwxrwx | README.md | 普通文件 | 说明文件       |
| rwxrwxrwx | bin       | 目录     | 可执行文件目录 |
| rwxrwxrwx | etc       | 目录     | 配置文件目录   |

`ASUS_ROUTER/script_bootloader/usr/shadowsocks/bin/`

| 权限      | 名称                 | 属性     | 说明                                       |
| --------- | -------------------- | -------- | ------------------------------------------ |
| rwxrwxrwx | shadowsocks_install         | 普通文件 | 安装文件                                   |
| rwxrwxrwx | ss_iptables         | 普通文件 | 插件的可执行程序，用于配置防火墙（未完成）    |
| rwxrwxrwx | ss_local_enable.service  | 普通文件 | 插件的可执行程序，用于启动程序 |
| rwxrwxrwx | ss_local_disable.service | 普通文件 | 插件的可执行程序，用于结束程序 |
| rwxrwxrwx | ss_redir_enable.service  | 普通文件 | 插件的可执行程序，用于启动程序（未完成） |
| rwxrwxrwx | ss_redir_disable.service | 普通文件 | 插件的可执行程序，用于结束程序（未完成） |
| rwxrwxrwx | ss_server_enable.service  | 普通文件 | 插件的可执行程序，用于启动程序（未完成） |
| rwxrwxrwx | ss_server_disable.service | 普通文件 | 插件的可执行程序，用于结束程序（未完成） |
| rwxrwxrwx | ss_tunnel_enable.service  | 普通文件 | 插件的可执行程序，用于启动程序（未完成） |
| rwxrwxrwx | ss_tunnel_disable.service | 普通文件 | 插件的可执行程序，用于结束程序（未完成） |

`ASUS_ROUTER/script_bootloader/usr/shadowsocks/etc/`

| 权限      | 名称         | 属性     | 说明                       |
| --------- | ------------ | -------- | -------------------------- |
| rwxrwxrwx | config_local.json | 普通文件 | ss_local_enable.service的配置文件 |

## 安装方法

执行`/tmp/mnt/ASUS_ROUTER/script_bootloader/usr/shadowsocks/bin/shadowsocks_install`

## 调用方法

| 插件文件             | 插件调用者                   | 调用位置    |
| -------------------- | ---------------------------- | ----------- |
| ss_local_enable.service | list_of_user_custom_scripts | 53行起（安装后需手动配置开机加载） |
| ss_local_disable.service | script_bootloader_usb_umount | 自动调用 |

## 需修改部分

`shadowsocks/etc/config_local.json`

| 行号 | 代码                         | 说明                   |
| ---- | ---------------------------- | ---------------------- |
| 29   | `"server":`  | Shadowsocks服务器IP地址        |
| 33   | `"server_port":`           | Shadowsocks服务器监听端口  |
| 37   | `"local_port":`           | 本地监听端口               |
| 37   | `"password":`           | 密码               |