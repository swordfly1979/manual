# 生成公钥和私钥

```bash
ssh-keygen 
	#命令用来生成公钥和私钥
    #-t 用来指定密钥类型（dsa | ecdsa | ed25519 | rsa | rsa1）
    #-p 用来指定密码短语
    #-C 用来添加注释
#示例
ssh-keygen -t rsa -C "mykey"
```

> 此时，会在存放ssh秘钥的地方生成两个文件（linux系统为/root/.ssh/），.pub结尾的是公钥，另一个是私钥

# 将公钥部署到服务器

```bash
#上传公钥到服务器
sftp root@yourhost -p 22
put mykey.pub 
#将文件写入authorized_keys中
cat mykey.pub >> ~/.ssh/authorized_keys
#修改公钥权限
chmod 600 ~/.ssh/authorized_keys
```

# 设置服务器ssh的可以通过公钥登录

```bash
#打开/etc/sshd_config文件，修改如下配置
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile  .ssh/authorized_keys #设置公钥文件，默认即可
#重启ssh服务
sudo service ssh restart
```

# ssh客户端登录

```bash
#方式一：ssh命令直间登录

ssh usernama@ip_address
#方式二：ssh客户端配置文件登录

	#1.在~/.ssh/目录下创建一个config文件，在config中写入相应的配置
        # Host 主机别名
        # HostName 主机地址
        # User 登陆用户名
        # Port 端口号
    #2.ssh<主机别名> 直接连接服务器
    ssh hostName
    #3.退出远程主机
    exit
```

# 用户登录设置

```bash
#禁止用户登录
chsh user -s /sbin/nologin
#允许用户登录
chsh user -s /bin/bash
#查看用户（/sbin/nologin即为不允许登录）
cat /etc/passwd
#查看用户密码
cat /etc/shadow
#所有系统用户密码都是 "!!" 或 "*"，代表没有密码是不能登录的。当然新创建的用户如果不设定密码，那么它的密码项也是 "!!"，代表这个用户没有密码，不能登录。
```

### 开启www用户使用密钥连接ssh

```bash
#允许www用户登录
chsh www -s /bin/bash
#home目录创建www/.ssh目录（并更改www及子目录所有者为www:www）
mkdir /home/www/.ssh
chown -R /home/www
#添加公钥文件
vi authorized_keys
chown www:www authorized_keys
chmod 400 authorized_keys
```



## 禁止特定条件使用密码登录

> 可以通过配置 /etc/ssh/sshd_config 文件来实现对特定对象的登录设置。一般 Match 区块添加在 sshd_config 文件末尾
>
> Match 关键字支持的条件包括 User, Group, Host 和 Address，条件样式是单个字符串，多个样式使用逗号分隔，也可以使用通配符（*）和求反符号（!）。

```bash
#禁止用户 foo，用户组 bar 使用口令登录
Match User foo, Group bar
    PasswordAuthentication no
#禁止除用户 foo 以外其他用户使用口令登录
Match User *, !foo
    PasswordAuthentication no
```

