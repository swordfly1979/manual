# 域名证书目录及说明

> oneinstack域名证书在/root/.acme.sh目录下。主要配置及已申请的域名证书都在此目录。后期如需修改，在此处修改相关目录配置文件即可
>
> **不用的网站在此处手动删除相关网站目录即可**

```bash
#证书手动更新命令
/root/.acme.sh/acme.sh --cron --home "/root/.acme.sh" --force
# --home 指定acme.sh的主目录
# --force 强制安装、强制证书续订或覆盖sudo限制。
# --cron 运行cron job以续订所有证书。
# 更多参数说明查看 https://the-x.cn/cmdtools/acme.sh.aspx
```

> 证书配置文件中 Le_Webroot=" " 配置指向的目录为访问到网站的根目录。如果网站做了转向（如301跳转），此目录一定为跳转后所指向的目录。否则域名证书验证无法通过

acme.sh官网查看具体使用说明 https://github.com/acmesh-official/acme.sh

