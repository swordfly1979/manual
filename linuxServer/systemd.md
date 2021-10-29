# systemctl 常用管理命令

```bash
#如何启动、关闭、启用/禁用服务
systemctl start vsftpd.service	#启动服务
systemctl stop vsftpd.service   #关闭服务
systemctl restart vsftpd.service	#重启服务
systemctl status vsftpd.service		#显示服务的状态
systemctl enable vsftpd.service		#在开机时启用服务
systemctl disable vsftpd.service	#在开机时禁用服务
systemctl is-enabled vsftpd.service		#查看服务是否开机启动
systemctl list-unit-files|grep enabled	#查看已启动的服务列表
systemctl --failed		#查看启动失败的服务列表
```

# update-rc.d 命令

> 此命令用于安装或移除System-V风格的初始化脚本连接。脚本是存放在 --- /etc/init.d/ ---目录下的，当然可以在此目录创建连接文件连接到存放在其他地方的脚本文件。
> 此命令可以指定脚本的执行序号，序号的取值范围是 0-99，序号越大，越迟执行。

### 用法

```bash
#加入开机启动项目中
update-rc.d myScript defaults
#删除开机启动项目
update-rc.d -f myScript remove
update-rc.d [-n] [-f] name remove #用于移除脚本。
update-rc.d [-n] name default [NN | SS KK] #NN表示执行序号（0-99），SS表示启动时的执行序号，KK表示关机时的执行序号，SS、KK主要用于在脚本直接的执行顺序上有依赖关系的情况下。
```

### 选项

-n：不做任何事情，只显示将要做的。（预览、做测试）
-f：强制移除符号连接，即使 /etc/init.d/script-name 仍然存在。

### 示例

```bash
#添加启动项
sudo update-rc.d   apache2 defaults  
sudo update-rc.d   nginx defaults  
sudo update-rc.d   redis\_6379 defaults
#删除启动项
sudo update-rc.d -f apache2 remove  
sudo update-rc.d -f nginx remove  
sudo update-rc.d -f redis\_6379 remove
```

