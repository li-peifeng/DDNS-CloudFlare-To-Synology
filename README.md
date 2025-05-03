<p align="center">
  <a href="https://peifeng.li"><img width="184px" alt="logo" src="https://cdn.jsdelivr.net/gh/li-peifeng/static/logo.png" />
  </a>
</p>

# Synology Cloudflare DDNS 脚本

此脚本添加 [Cloudflare](https://www.cloudflare.com/) DDNS 到 [Synology](https://www.synology.com/) NAS. 此脚本使用 Cloudflare API v4.

## 如何使用

### 连接到 Synology SSH

1. 登录 DSM
2. 导航到 控制面板 > Terminal & SNMP > 打开 SSH 服务
3. 使用任意SSH客户端连接到 Synology.
4. 需使用 Synology 管理员账户.

### 在 Synology 运行脚本

1. 下载 `cloudflareddns.sh` 到 `/usr/syno/bin/ddns/cloudflare.sh`

```
wget https://github.com/li-peifeng/DDNS-CloudFlare-To-Synology/master/cloudflareddns.sh -O /usr/syno/bin/ddns/cloudflare.sh
```

`/usr/syno/bin/ddns/cloudflare.sh` 这路径不是强制的，你可以随意输入。如果你将脚本放在其他名称或路径中，请确保使用正确的路径。

2. 授予执行权限

```
chmod +x /usr/syno/bin/ddns/cloudflare.sh
```

3. 添加 `cloudflareddns.sh` 到 Synology

```
cat >> /etc.defaults/ddns_provider.conf << 'EOF'
[Cloudflare]
        modulepath=/usr/syno/bin/ddns/cloudflare.sh
        queryurl=https://www.cloudflare.com
        website=https://www.cloudflare.com
E*.
```

### 获取 Cloudflare 配置参数

1. 转到您的域名概览页面并复制您的区域 ID。
2. 转到您的个人资料 > **API 令牌** > **创建 令牌**. 它应该具有“区域 > DNS > 编辑”的权限。复制 api 令牌。

### 设置 DDNS

1. 登录 DSM
2. 导航到控制面板 > 外部访问 > DDNS > 新增
3. 输入以下内容:
   - 服务商: `Cloudflare`
   - 主机: `www.example.com`
   - 用户名/Email: `<Zone ID>`
   - 密码: `<API Token>`
