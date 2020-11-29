| | |
|-|-|
| 服务器 | 阿里云 |
| 编码平台 | Cloud Studio |

# 服务器部署

## 服务器初始化

### [阿里云控制台](https://ecs.console.aliyun.com/#/home)
1. 阿里云控制台 -> 云服务器ECS -> 点击名称
2. 服务器相关设置
    - 实例详情→启动关闭服务器
    - 安全组→端口设置
        > **初始安全组**（系统自带）：**22/22(SSH)**, 3389/3389(RDP), -1/-1     
        > **自定义安全组**：**HTTP(80)**, **HTTPS(443)**, **MySQL(3306)**, telnet(23), MS SQL(1433), Oracle(1521), PostgreSQL(5432), Redis(6379)
    - 云盘→初始化
    - 快照

## 服务器远程工具
| 名称 | 下载地址 | 作用 |
|-|-|-|
| WinSCP | https://winscp.net/eng/download.php | 文件传输 |
| PuTTY | https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html | 服务器命令行 |


------------------------------------------------------------------------------------------


# 开发环境配置

## 安装环境与环境配置(CentOS7)
| | | |
|-|-|-|
| Cloud Studio | ```~/.ssh/authorized_keys``` | 配置开发环境：复制ssh码，或者密码登录 |
| Git | ```yum install -y git``` | 版本控制 |
| node.js | https://nodejs.org/en/download/ | 开发环境 |
| Nginx | https://nginx.org/en/download.html | 服务器工具 |
| MySQL |  | 数据库 |


----------------------------------------------------------------------------------------------


## Git的安装
> ```yum install -y git```

## nodejs的安装
1. 下载文件(Linux Binaries(x64))
    > https://nodejs.org/en/download/
2. 使用WinSCP工具移动文件到目录```/home/yoosonchan/```
3. 解压
    > ```tar -xvf node-v14.15.1-linux-x64.tar.xz```     
    > 版本号不同文件名不同      

    > 解压后压缩包可删除```rm```命令
4. 移动至```/usr/local```
    > 进入安装目录： ```cd /usr/local/```

    > 移动已解压文件到安装目录： ```mv /home/yoosonchan/node-v14.15.1-linux-x64 . ```       
        >> 后面的```.```表示移动到当前目录
    
    > 更改目录名： ```mv node-v14.15.1-linux-x64/ nodejs```
5. 配置node全局变量
    > 软链接方式
    ```
    ln -s /usr/local/nodejs/bin/npm /usr/local/bin/
    ln -s /usr/local/nodejs/bin/node /usr/local/bin/
    ```
6. 测试是否安装成功
    ```
    node -v
    npm -v
    ```


-----------------------------------------------------------------------------


## Nginx的安装
1. 安装```gcc```
    > ```yum install gcc-c++```
        >> Nginx 是 C语言 开发,安装 nginx 需要先将官网下载的源码进行编译，编译依赖 gcc 环境.

    > 阿里云服务器通常自带，可以通过```gcc -v```测试是否有安装，若有忽略第一步
2. 安装```pcre```，```pcre-devel```
    > ```yum install -y pcre pcre-devel```
        >> pcre(Perl Compatible Regular Expressions)是一个perl库，包括perl兼容的正则表达式库，nginx的http模块使用pcre来解析正则表达式，所以需要安装pcre库，pcre-devel 是使用 pcre 开发的一个二次开发库。nginx也需要此库。
3. 安装```zlib```
    > ```yum install -y zlib zlib-devel```
        >> zlib 库提供了很多种压缩和解压缩的方式， nginx 使用 zlib 对 http 包的内容进行 gzip ，所以需要在 Centos 上安装 zlib 库.
4. 安装```OpenSSL```
    > ```yum install -y openssl openssl-devel```
        >> OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及 SSL 协议，并提供丰富的应用程序供测试或其它目的使用。      
        nginx 不仅支持 http 协议，还支持 https（即在ssl协议上传输http），所以需要在 Centos 安装 OpenSSL 库。
5. 安装```Nginx```
    - 官网查看最新安装包版本（**Stable version**）, 记住版本号.
        > https://nginx.org/en/download.html
    - 下载安装包（```wget```下载）
        - 确保下载```wget```,若未下载，使用```yum install wget```安装。
        - ```wget```下载```Nginx```
            > ```wget -c https://nginx.org/download/nginx-1.18.0.tar.gz```
                >> 根据实际情况输入版本号
    - 解压
        > ```tar -zxvf nginx-1.18.0.tar.gz```             
        > ```cd nginx-1.18.0```
    - 配置（在```Nginx```目录下）
        > ```./configure```
    - 编译安装
        > ```make```        
        > ```make install```        

        > 注：解压和安装完成后压缩包和安装目录可删除```rm```（删除文件）和```rm -rf```（删除目录）命令
    - 进入```Nginx```安装目录
        > 查找```Nginx```安装目录：```whereis nginx```      
        > 进入安装目录：```cd /usr/local/nginx```
    - 配置配置文件（```nginx.conf```文件）
        > 查看监听端口```listen 80```是不是80，也可设置为其他
    - 启动```Nginx```服务
        > 进入目录: ```cd /usr/local/nginx/sbin```      
        > 启动：```./nginx```
            >> ```./nginx -s stop```：停止命令（此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程）      
            >> ```./nginx -s quit```：停止命令（此方式停止步骤是待nginx进程处理任务完毕进行停止）      
            >> ```./nginx -s reload```：重启命令        
    - 查看是否启动成功
        > ```ps -ef | grep nginx```
    - 访问服务器地址验证是否成功
    - **开机自启动**（配置```rc.local```文件）
        > ```vi /ect/rc.local```        
        > 添加代码：```/usr/local/nginx/sbin/nginx```       
        > 设置权限：```chmod 755 rc.local```


--------------------------------------------------------------------------------

