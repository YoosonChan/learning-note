# 域名解析

1. 进入[阿里云域名控制台](https://dc.console.aliyun.com/)
2. 点击相对应的域名的解析按钮
3. 添加记录
    - **新手引导**
        > 直接输入记录值，即服务器IP地址即可
    - 记录类型
        | 名称 | 说明 |
        |-|-|
        | A | 将域名指向一个IPV4地址|
        | CNAME | 将域名指向另外一个域名 |
        | AAAA | 将域名指向一个IPV6地址 |
        | NS | 将子域名指定其他DNS服务器解析 |
        | MX | 将域名指向邮件服务器地址 |
        | SRV | 记录提供特定的服务的服务器 |
        | TXT | 文本长度限制512.通常做SPF记录(反垃圾邮件) |
        |CAA |  CA证书颁发机构授权校验 |
        | 显性URL | 将域名重定向到另外一个地址 |
        | 隐性URL | 与显性URL类似，但是会隐藏真实目标地址 |
    
    - 主机记录
        > 主机记录就是域名前缀。常见用法有:

        | 名称 | 说明 |
        |-|-|
        | www | 解析后的域名为ww.ljyun.com. |
        | @ | 直接解析主域名aliyun.com. |
        | * | 泛解析.匹配其他所有域名*aljun.com. |
        | mail | 将域名解析为mailaliyun.com. 通常用于解析邮箱服务器。 |
        | 二级域名 | 如: abaliyun.com.填写abC. |
        | 手机网站 | 如: maliyun.com. 填写m. |
        | 显性URL | 不支持泛解析(泛解析:将所有子域名解析到同一地址) |
    - 记录值(通常为服务器IP地址)
        > 显性URL记录值请填写要跳转到的网址，例如https://www.aliyun.com     
        > URL转发功能目前只支持网站有备案号且接入商是万网的域名转发需求     
        > URL转发的目标域名不支持中文域名
    - TTL

# Nginx中配置域名（nginx.conf）
## 新增配置结构
```
server 
{ 
	listen      80;     # 80端口监听
	server_name example.com;  # 域名
	location / {
	    index index.htm index.html index.php; 
	    root /home/www/xxx;   # 初始页面在本地的目录位置，即路径
	}
}
```