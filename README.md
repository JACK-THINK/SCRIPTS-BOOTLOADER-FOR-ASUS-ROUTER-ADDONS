# SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER-ADDONS

## 介绍

本项目是适用于[SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER](https://github.com/JACK-THINK/SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER)系统的插件库

## 文件结构

1. 每个目录均是一个独立插件
2. 每个插件均含有README文件，详述了该插件的
   - 概述
   - 安装前提
   - 文件结构
   - 安装方法
   - 调用方法
   - 需修改部分

## 安装方法

1. 安装[SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER](https://github.com/JACK-THINK/SCRIPTS-BOOTLOADER-FOR-ASUS-ROUTER)系统
2. 按次序安装并启用下列插件
   - swap
   - entware
   - development_tools
3. 将所需插件目录存放至`script_bootloader/usr/`目录下
4. 执行插件`bin`目录中的`*_install`（若有）安装插件
5. 更改`script_bootloader/bin/list_of_user_custom_scripts`文件，在66行起插入需启用的插件路径