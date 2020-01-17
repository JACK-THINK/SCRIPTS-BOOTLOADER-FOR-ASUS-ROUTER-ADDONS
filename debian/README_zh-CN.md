# Readme for debian

## 概述

1. 本插件用于安装、卸载debian，并运行基于debian的服务
2. 安装本插件后，可直接在路由器上开启debian环境，安装海量软件（远多于entware）
3. 提供两种安装程序
   - `debian_install`：预安装版安装程序，默认启用
   - `debian_install_online`：官方部署安装程序，非常耗时

## 安装前提

1. 必须安装并启用entware和monit

## 文件结构

`ASUS_ROUTER/script_bootloader/usr/debian/`

| 权限      | 名称            | 属性     | 说明             |
| --------- | --------------- | -------- | ---------------- |
| rwxrwxrwx | README_zh-CN.md | 普通文件 | 说明文件         |
| rwxrwxrwx | bin             | 目录     | 可执行文件目录   |
| rwxrwxrwx | etc             | 目录     | 配置文件目录     |
| rwxrwxrwx | usr             | 目录     | 外部软件资源目录 |

`ASUS_ROUTER/script_bootloader/usr/debian/bin/`

| 权限      | 名称                  | 属性     | 说明             |
| --------- | --------------------- | -------- | ---------------- |
| rwxrwxrwx | debian_install        | 普通文件 | 预安装版安装程序 |
| rwxrwxrwx | debian_install_online | 普通文件 | 官方部署安装程序 |
| rwxrwxrwx | debian_uninstall      | 普通文件 | 插件的卸载程序   |
| rwxrwxrwx | debian                | 普通文件 | 插件的主程序     |

`ASUS_ROUTER/script_bootloader/usr/debian/etc/`

| 权限      | 名称                 | 属性     | 说明            |
| --------- | -------------------- | -------- | --------------- |
| rwxrwxrwx | monit.d/debian       | 普通文件 | monit.d配置文件 |

`ASUS_ROUTER/script_bootloader/usr/debian/usr/`

| 权限      | 名称                       | 属性     | 说明           |
| --------- | -------------------------- | -------- | -------------- |
| rwxrwxrwx | debian-jessie-armel.tar.gz | 普通文件 | debian预安装包 |
| rwxrwxrwx | debian-buster-arm64.tar.gz | 普通文件 | debian预安装包 |

## 安装方法

执行`/tmp/mnt/ASUS_ROUTER/script_bootloader/usr/debian/bin/debian_install`

   > [受支持的路由器型号](https://github.com/Entware/Entware/wiki/Install-on-Asus-stock-firmware)：
   >
   > | 架构        | 路由器型号                                                                                                                                                        |
   > | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
   > | **aarch64** | GT-AC2900, GT-AC5300, GT-AX11000, RT-AC86U, RT-AX88U, RT-AX92U                                                                                                    |
   > | **armv7**   | Lyra Voice, RT-AC56U, RT-AC66U B1, RT-AC68P, RT-AC68U, RT-AC87U, RT-AC88U, RT-AC1200G, RT-AC1900P, RT-AC3100, RT-AC3200, RT-AC5300, RT-ACRH13, RT-AX56U, RT-AX58U |

## 卸载方法

执行`cd /tmp && /opt/bin/debian stop && /tmp/mnt/ASUS_ROUTER/script_bootloader/usr/debian/bin/debian_uninstall`

## 调用方法

1. 由entware自动执行
2. 执行`debian enter`进入Debian环境
3. 在Debian环境中，执行`exit`退出Debian环境