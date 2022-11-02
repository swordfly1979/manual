# nodejs安装

> 官网下载需要安装的包，环境变量添加 path（安装路径）/bin即可

## 更新及切换版本

~~~bash
#清理npm cache
npm cache clean -f
#全局安装n
npm install -g n
# n命令
    n #列出所有安装的版本供你切换
    n latest #安装最新版本
    n stable #安装最新稳定版
    n lts #安装最新长期支持版本
    n rm [版本号] #删除某一版本
    n -h #帮助命令
    n [版本号] #安装指定版本node
#通过N_PREFIX变量来修改n的默认node安装路径
export N_PREFIX=/home/node-v6.9.0-linux-x64/ #自己定义的node实际安装位置
~~~

# pm2安装

```bash
npm i pm2 -g
```

## pm2常用命令

```bash
#查看pm2运行列表
pm2 list
#添加服务(注意-- run中间有空格)
pm2 start npm --name "your app name" -- run start
#起动或停止pm2
pm2 stop app name|app id
```



