# Readme for l2tp

## 概述

1. 本插件用于配置、启动和结束l2tp客户端

## 安装前提

1. 无

## 文件结构

`ASUS_ROUTER/script_bootloader/usr/l2tp/`

| 权限      | 名称      | 属性     | 说明             |
| --------- | --------- | -------- | ---------------- |
| rwxrwxrwx | README.md | 普通文件 | 说明文件         |
| rwxrwxrwx | bin       | 目录     | 可执行文件目录   |
| rwxrwxrwx | tmp       | 目录     | 临时文件目录 |

`ASUS_ROUTER/script_bootloader/usr/l2tp/bin/`

| 权限      | 名称                 | 属性     | 说明                                                         |
| --------- | -------------------- | -------- | ------------------------------------------------------------ |
| rwxrwxrwx | l2tp_enable.service  | 普通文件 | 插件的可执行程序，用于启动程序                               |
| rwxrwxrwx | l2tp_disable.service | 普通文件 | 插件的可执行程序，用于结束程序                               |

`ASUS_ROUTER/script_bootloader/usr/l2tp/tmp/`

| 权限      | 名称         | 属性     | 说明                       |
| --------- | ------------ | -------- | -------------------------- |
| rwxrwxrwx | routes_to_disable.tmp | 普通文件 | 结束时自动生成 |

## 安装方法

无需安装

## 调用方法

| 插件文件                          | 插件调用者                   | 调用位置  |
| --------------------------------- | ---------------------------- | --------- |
| l2tp_enable.service | list_of_user_custom_scripts  | 53行起（安装后需手动配置开机加载） |
| l2tp_disable.service | script_bootloader_usb_umount | 自动调用 |

## 需修改部分

`l2tp/bin/l2tp_enable.service`

| 行号 | 代码                         | 说明                   |
| ---- | ---------------------------- | ---------------------- |
| 32   | `SERVER_IP_ADDRESS=""`  | VPN服务器IP        |
| 35   | `USERNAME=""`           | L2TP用户名               |
| 38   | `PASSWORD=""`           | L2TP密码               |