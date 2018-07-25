# Readme for iptables_rules

## 概述

1. 本插件用于配置、启动和结束iptables_rules
2. 安装本插件后，可将防火墙规则写入相应文件，固化规则

## 安装前提

1. 无

## 文件结构

`ASUS_ROUTER/script_bootloader/usr/iptables_rules/`

| 权限      | 名称      | 属性     | 说明           |
| --------- | --------- | -------- | -------------- |
| rwxrwxrwx | README.md | 普通文件 | 说明文件       |
| rwxrwxrwx | bin       | 目录     | 可执行文件目录 |

`ASUS_ROUTER/script_bootloader/usr/iptables_rules/bin/`

| 权限      | 名称                                          | 属性     | 说明                           |
| --------- | --------------------------------------------- | -------- | ------------------------------ |
| rwxrwxrwx | iptables_rules_primary_router_enable.service  | 普通文件 | 插件的可执行程序，用于启动程序 |
| rwxrwxrwx | iptables_rules_primary_router_disable.service | 普通文件 | 插件的可执行程序，用于结束程序 |

## 安装方法

无需安装

## 调用方法

| 插件文件                          | 插件调用者                   | 调用位置  |
| --------------------------------- | ---------------------------- | --------- |
| iptables_rules_primary_router_enable.service  | list_of_user_custom_scripts | 66行起（安装后需手动配置开机加载） |
| iptables_rules_primary_router_disable.service | script_bootloader_usb_umount | 自动调用 |

## 需修改部分

`iptables_rules/bin/iptables_rules_primary_router_enable.service`

| 行号 | 说明             |
| ---- | ---------------- |
| 第41行起 | iptables规则语句 |

`iptables_rules/bin/iptables_rules_primary_router_disable.service`

| 行号 | 说明                 |
| ---- | -------------------- |
| 第31行起 | iptables规则删除语句 |