＃ ssh-config配置 ＃

> 转自：http://zlong.org/2015/06/08/ssh-config/

之前遇到这样的一个问题：我有两个github账号，一台电脑上都要访问这两个账号，都使用ssh key认证方式，该怎么配置ssh?

## ssh的配置文件 ##

ssh client有两个配置文件，/etc/ssh/ssh_config和~/.ssh/config，前者是对所有用户，后者是针对某个用户，两个文件的格式是一样的。

## ssh配置文件的格式 ##

每一行是一个配置项，如下：

```
config value
config value1 value2
```

也可以使用=号：

```
config=value
config=value1 value2
```

空行和以#开头的行会被忽略；
所有的值是区分大小写的，但参数名不区分。

## 示例 ##

通常情况下使用ssh连接服务器使用如下命令：

```
ssh username@server.com
```

这时会默认使用~/.ssh/id_rsa这个密钥，如果想使用不同的密钥则要：

```
ssh -i path/to/id_rsa username@server.com
```

如果不想每次都指定这些密钥、用户名、服务器地址的话，可以在~/.ssh/config中配置，如下：

```
Host server1
	HostName server.com
	User username
	IdentifyFile path/to/id_rsa
```

这样就可以简单的使用以下命令：

```
ssh server1
```

其实就相当于server1是个别名，可以任意取名。

在来看看最开始提出的问，有两个github账号，这时可以用ssh-keygen生成两个ssh密钥，~/.ssh/id_rsa1和~/.ssh/id_rsa2，~/.ssh/config，每个账号一个，配置如下：

```
Host github-user1
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa1

Host github-user2
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa2
```

使用git clone时就用如下命令：

```
git clone github-user1:user1/repo.git
git clone github-user2:user2/repo.git
```
