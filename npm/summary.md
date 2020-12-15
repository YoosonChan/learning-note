# 命令行
> [配置文件](https://docs.npmjs.com/cli/v6/configuring-npm/package-json)    
> [命令行](https://docs.npmjs.com/cli/v6/commands)

## 初始化
```sh
npm init
```

## 显示安装依赖
```sh
npm list [-g] [--depth 0]
```
> ```-g```：全局依赖
> ```--depth```：依赖树层数

## 修复依赖
```sh
npm audit fix
```

# centOS全局设置
## 查看npm全局源文件目录位置
```sh
npm root -g
# /usr/local/nodejs/lib/node_modules
```

## [使用```ln```命令同步文件链接](runoob.com/linux/linux-comm-ln.html)
```sh
# 系统全局地址
# /usr/local/bin/
```
### 以cpm为例
```sh
# 原始地址: /usr/local/nodejs/lib/node_modules/cnpm/bin
# 添加软链接
ln -s /usr/local/nodejs/lib/node_modules/cnpm/bin/cnpm /usr/local/bin/cnpm
```

# 淘宝镜像安装
> https://developer.aliyun.com/mirror/NPM?from=tnpm
你可以使用我们定制的 ```cnpm``` (```gzip``` 压缩支持) 命令行工具代替默认的 ```npm```:
```sh
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```
或者你直接通过添加 ```npm``` 参数 ```alias``` 一个新命令:
```sh
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"

# Or alias it in .bashrc or .zshrc
$ echo '\n#alias for cnpm\nalias cnpm="npm --registry=https://registry.npm.taobao.org \
  --cache=$HOME/.npm/.cache/cnpm \
  --disturl=https://npm.taobao.org/dist \
  --userconfig=$HOME/.cnpmrc"' >> ~/.zshrc && source ~/.zshrc
```