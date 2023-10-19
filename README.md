# Cloudflare DDNS for Synology

在群晖 DSM 7.x 上 `控制面板-> 外部访问-> DDNS` 使用Cloudflare

### 通过SSH访问群晖

1. 登录你的DSM
2. 打开并勾选 `控制面板-> 终端机和 SNMP > 启动 SSH 功能`
3. 使用终端设备(例如Xshell) 访问群晖SSH.
4. 使用你的群晖账户登录SSH
5. 输入 `sudo -i` 并输入root账户密码, 提权到 `root` 权限

### 在SSH中运行命令

1. 从本项目下载对应的 `cloudflare-ddns-v*.sh` 文件到 `/sbin/cloudflare-ddns-v*.sh`

## IP v4

```shell
wget https://raw.githubusercontent.com/QAQQL/cloudflare-ddns-for-synology/main/cloudflare-ddns-v4.sh -O /sbin/cloudflare-ddns-v4.sh
# 访问不了可以使用代理站,命令如下
# wget https://ghproxy.com/https://raw.githubusercontent.com/QAQQL/cloudflare-ddns-for-synology/main/cloudflare-ddns-v4.sh -O /sbin/cloudflare-ddns-v4.sh
```

2. 授予脚本文件执行权限

```shell
chmod +x /sbin/cloudflare-ddns-v4.sh
```

3. 添加 `cloudflare-ddns-v4.sh` 到群晖DDNS

```shell
cat >> /etc.defaults/ddns_provider.conf << 'EOF'
[Cloudflare IPv4]
        modulepath=/sbin/cloudflare-ddns-v4.sh
        queryurl=https://www.cloudflare.com
        website=https://www.cloudflare.com
EOF

```

## IP v6 (可选)

```shell
wget https://raw.githubusercontent.com/QAQQL/cloudflare-ddns-for-synology/main/cloudflare-ddns-v6.sh -O /sbin/cloudflare-ddns-v6.sh
# 访问不了可以使用代理站,命令如下
# wget https://ghproxy.com/https://raw.githubusercontent.com/QAQQL/cloudflare-ddns-for-synology/main/cloudflare-ddns-v6.sh -O /sbin/cloudflare-ddns-v6.sh
```

2. 授予脚本文件执行权限

```shell
chmod +x /sbin/cloudflare-ddns-v6.sh
```

3. 添加 `cloudflare-ddns-v6.sh` 到群晖DDNS

```shell
cat >> /etc.defaults/ddns_provider.conf << 'EOF'
[Cloudflare IPv6]
        modulepath=/sbin/cloudflare-ddns-v6.sh
        queryurl=https://www.cloudflare.com
        website=https://www.cloudflare.com
EOF

```

## 获取Cloudflare参数

1. 访问您的域概述页面并复制您的`区域ID`  =>  `<Zone ID>`
2. 访问 [用户 API 令牌](https://dash.cloudflare.com/profile/api-tokens) 页面, 拷贝 `API 密钥` (`Global API Key`)  =>  `<API Token>`
3. 访问 [个人资料](https://dash.cloudflare.com/profile) 页面, 拷贝 `电子邮件地址`  =>  `<Cloudflare Email>`

### 配置 DDNS

1. 登录 DSM
2. 打开 `控制面板-> 外部访问-> DDNS-> 新增`
3.  输入以下内容:
   - 服务供应商: `Cloudflare IPv*`
   - 主机名称: `xxx.domainname.com`
   - 用户名/电子邮件: `<Zone ID>`
   - 密码/密钥: `<Cloudflare Email>|<API Token>`

感谢原项目 [joshuaavalon/SynologyCloudflareDDNS](https://github.com/joshuaavalon/SynologyCloudflareDDNS/) & [insistent-afk/cloudflare-ddns-for-synology](https://github.com/insistent-afk/cloudflare-ddns-for-synology)