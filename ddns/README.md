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
| rwxrwxrwx | Documents_Assets | 目录 | 说明文件资源目录         |
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

| 行号 | 代码               | 说明               |
| ---- | ------------------ | ------------------ |
| 10   | `DDNS_HOSTNAME=""` | 要使用的二级域名   |
| 14   | `DDNS_PASSWORD=""` | 上述域名的DDNS Key |

## 使用方法

> 1. 以下教程使用阿里云域名为例，其他提供商的域名管理方法大同小异，不另行作具体说明
> 2. 在域名服务商处购买的域名一般为顶级域名（格式为：`XXX.XXX`）

#### 配置DNS.HE.NET

1. 登录<https://dns.he.net>

   ![step1](./Documents_Assets/ddns/dns_he_net_configuration/step1.png)

2. 单击“Add a new domain”

   ![step2](./Documents_Assets/ddns/dns_he_net_configuration/step2.png)

3. 在“Domain Name”中，填入将要使用的顶级域名（格式为：`XXX.XXX`）并单击“Add Domain!”

   ![step3](./Documents_Assets/ddns/dns_he_net_configuration/step3.png)

4. 页面提示“域名添加成功”

   ![step4](./Documents_Assets/ddns/dns_he_net_configuration/step4.png)

#### 修改域名DNS服务器

1. 登录域名管理控制台，找到要使用的域名，单击“管理”

   ![step1](./Documents_Assets/ddns/domain_configuration/step1.png)

2. 在该域名管理页面中，单击“修改DNS”

   ![step2](./Documents_Assets/ddns/domain_configuration/step2.png)

3. 在DNS管理页面中，单击“修改DNS服务器”

   ![step3](./Documents_Assets/ddns/domain_configuration/step3.png)

4. 将该域名的默认DNS服务器变更为HE.NET提供的DNS服务器

   ![step4](./Documents_Assets/ddns/domain_configuration/step4.png)

5. 修改完成后，需等待2-24小时，方可生效

#### 添加DDNS记录

1. 找到新添加的域名，单击下图红框处“Edit”图标

   ![step5](./Documents_Assets/ddns/dns_he_net_configuration/step5.png)

2. 单击“New A”

   ![step6](./Documents_Assets/ddns/dns_he_net_configuration/step6.png)

3. 填入如下内容并单击“Submit”

   > - Name：填入要使用的二级域名（格式为：`XXX.XXX.XXX`）
   > - IPv4 Address：随便填入一个IP地址，默认为本机IP
   > - TTL (Time to live)：5 minutes
   > - Enable entry for dynamic dns：必选

   ![step7](./Documents_Assets/ddns/dns_he_net_configuration/step7.png)

4. 单击“Generate a DDNS key”图标

   ![step8](./Documents_Assets/ddns/dns_he_net_configuration/step8.png)

5. 单击“Generate a key”后，两个文本框内会自动填写“DDNS Key”，**记录**并单击“Submit”

   ![step9](./Documents_Assets/ddns/dns_he_net_configuration/step9.png)

6. 见[需修改部分](#需修改部分)，按说明填入相关信息