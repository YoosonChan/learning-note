# SSL证书部署
[阿里云SSL证书管理控制台](https://yundun.console.aliyun.com/?spm=5176.12818093.0.2.4cbd16d0pMoqX6&p=cas#/overview/cn-hangzhou)

> 事先在服务器安全组中添加HTTPS(443)规则

1. 点击部署，选择自己服务器

2. 下载服务器类型证书（```Nginx```）
    - 点击帮助查看文档
    - 点击下载证书

## [在Nginx或Tengine服务器上安装证书](https://help.aliyun.com/document_detail/98728.html)

阿里云SSL证书服务支持下载证书并安装到Nginx、Tengine服务器上。本文介绍了安装证书的具体操作。

**前提条件**:
已准备好远程登录工具，例如PuTTY或者Xshell。

**背景信息**:
- 本文以CentOS 8、Nginx 1.14.1为例进行说明。由于版本不同，您在操作过程中的命令可能会略有区别。
- 本文中**证书名称**以```domain name```为例，例如，**证书文件名称**为```domain name.pem```、**证书密钥文件名称**为```domain name.key```。
- 下载的Nginx证书压缩文件解压后包含：
    - **PEM证书文件**。
    - **KEY证书密钥文件**。申请证书时如果未选择自动创建CRS，则下载的证书文件压缩包中不会包含KEY文件，需要您自己手动创建证书密钥文件。
> **说明** PEM证书文件是采用Base64编码的文本文件，您可根据需要修改成其他扩展名。关于证书格式的详细内容，请参见[主流数字证书都有哪些格式](https://help.aliyun.com/knowledge_detail/42214.html#concept-a4g-mbv-ydb)。


----------------------------


## 操作步骤
1. 登录阿里云SSL证书控制台。
2. 在左侧导航栏，单击概览。
3. 在SSL证书页面，定位到需要下载的证书实例，单击下载。
4. 在证书下载页面，定位到Nginx服务器，单击右侧操作列的下载，将Nginx服务器证书压缩包下载到本地。
5. 解压已下载保存到本地的Nginx证书压缩包文件。

    解压后的文件夹中有2个文件：
    - **证书文件**：文件类型为```PEM```。
    - **密钥文件**：文件类型为```KEY```。
6. 登录您的Nginx服务器，在Nginx安装目录（默认为```/usr/local/nginx/conf```）执行以下命令，创建cert目录：
    ```shell
    cd /usr/local/nginx/conf  #进入Nginx默认安装目录。此处为Nginx默认安装目录，请您根据实际配置情况操作。
    mkdir cert  #创建cert证书目录。
    ```
7. 使用远程登录工具（例如```PuTTY```或者```Xshell```）附带的本地文件上传功能，将下载的证书文件和密钥文件上传到Nginx服务器的cert目录下。
    > **说明**: 如果您在申请证书时选择手动创建```CSR文件```，请将您自己手动创建的证书密钥文件上传到```cert```目录下，并命名为```domain name.key```。

8. 执行以下命令，打开Nginx安装目录```/conf/nginx.conf```配置文件并进行编辑。
    ```shell
    vim /usr/local/nginx/conf/nginx.conf #打开配置文件。此处为Nginx默认配置文件目录，请您根据实际配置情况操作。
    ```
    按i键进入编辑模式，在配置文件中找到HTTP协议代码片段，在HTTP协议代码里面新增以下server配置示例。如果server配置已存在，按照以下注释内容修改相应的配置即可。

    ```shell
    #以下属性中以ssl开头的属性代表与证书配置有关，其他属性请根据自己的需要进行配置。
    server {
         listen 443 ssl; #配置HTTPS的默认访问端口号为443。此处如果未配置HTTPS的默认访问端口，可能会造成Nginx无法启动。Nginx 1.15.0以上版本请使用listen 443 ssl代替listen 443和ssl on。
         server_name www.certificatestests.com; #将www.certificatestests.com修改为您证书绑定的域名，例如：www.example.com。如果您购买的是通配符域名证书，要修改为通配符域名，例如：*.aliyun.com。
         root html;
         index index.html index.htm;
         ssl_certificate cert/domain name.pem;  #将domain name.pem替换成您证书的文件名称。
         ssl_certificate_key cert/domain name.key; #将domain name.key替换成您证书的密钥文件名称。
         ssl_session_timeout 5m;
         ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4; #使用此加密套件。
         ssl_protocols TLSv1 TLSv1.1 TLSv1.2; #使用该协议进行配置。
         ssl_prefer_server_ciphers on;
         location / {
         root html;  #站点目录。
         index index.html index.htm;
                    }
      }
      ```
      配置文件修改完毕之后，按```Esc```键后输入```:wq！```，然后按Enter键保存修改的配置文件并退出编辑模式。
9. 执行以下命令，进入Nginx服务器的可执行目录```sbin```并重启Nginx服务器。
    ```
    cd /usr/local/nginx/sbin  #进入Nginx服务器的可执行目录sbin。
    ./nginx -s reload  #重启Nginx服务器。
    ```
    > **说明**: 
    如果重启Nginx服务器出现```the "ssl" parameter requires ngx_http_ssl_module```报错，您需要重新编译Nginx并在编译安装的时候加上```--with-http_ssl_module```配置。
    如果重启Nginx服务器出现```"/cert/3970497_pic.certificatestests.com.pem":BIO_new_file() failed (SSL: error:02001002:system library:fopen:No such file or directory:fopen('/cert/3970497_pic.certificatestests.com.pem','r') error:2006D080:BIO routines:BIO_new_file:no such file)```报错，您需要去掉证书相对路径最前面的```/```。例如，您需要去掉```/cert/3970497_pic.certificatestests.com.pem```最前面的```/```，使用正确的相对路径```cert/3970497_pic.certificatestests.com.pem```。

10. **可选**：设置HTTP请求自动跳转HTTPS。

    在需要跳转的HTTP站点下添加以下rewrite语句，实现HTTP访问自动跳转到HTTPS页面。
    ```shell
    server {
        listen 443 ssl;
        server_name www.certificatestests.com; #将www.certificatestests.com修改为您证书绑定的域名，例如：www.example.com。
        rewrite ^(.*)$ https://$host$1 permanent;   #将所有HTTP请求通过rewrite重定向到HTTPS。
        location / {
            index index.html index.htm;
        }
    }
    ```

-----------------------------


## 解决重启Nginx服务器出现```the "ssl" parameter requires ngx_http_ssl_module```报错问题
> nginx缺少http_ssl_module模块，需要在已安装的nginx中添加ssl模块

- 查看```nginx```原有的模块
    > ```/usr/local/nginx/sbin/nginx -V```

    **结果**：```configure arguments```中没有模块

- 进入```nginx```源码包目录
    开始配置
    > ```./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module```

- 配置完成，开始编译
    > ```make```
    > 注意：不要使用```make install```，否则会覆盖安装

- 替换原有```nginx```
    - 替换之前先**备份**
        > ```cp /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx.bak```
    - **停止**```nginx```服务
        > 查询进程      
        > ```ps -ef | grep nginx```
        > 从容停止```Nginx```：```kill -QUIT 主进程号```        
        > 快速停止```Nginx```：```kill -TERM 主进程号```        
        > 强制停止```Nginx```：```pkill -9 nginx```
    - 将编译完成nginx**覆盖**原有nginx
        > ```cp ./objs/nginx /usr/local/nginx/sbin/```
- 查看结果:     
    ```/usr/local/nginx/sbin/nginx -V```
    
    **结果**：```configure arguments: --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module```