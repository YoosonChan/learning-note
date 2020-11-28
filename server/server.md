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


