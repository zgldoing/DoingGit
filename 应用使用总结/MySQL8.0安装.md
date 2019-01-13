---
typora-root-url: ..
---



# MySQL的安装

## MySQL8.0安装

### 1. 下载

- 进度[官网](https://dev.mysql.com/downloads/mysql/)下载,这里下载的是64位。
  ![MySQL下载](/应用使用总结/image/01_MySQL下载.png)
- 下载完后解压，路径如下：

![01_MySQL解压文件夹](/应用使用总结/image/02_MySQL解压文件夹.png)


- 配置环境变量

> 可以将解压后的文件直接复制到其他文件夹，或者改文件夹D:\MySQL\mysql-8.0.13-winx64名为其他名字。
>
> 配置环境变量Path指向MySQL的bin文件夹即可。

![03_MySQL配置环境变量](/应用使用总结/image/03_MySQL配置环境变量.png)


- 配置初始化的my.ini文件的文件

> 解压后的目录并没有的my.ini文件，没关系可以自行创建在安装根目录下添加的my.ini（新建文本文件，将文件类型改为的.ini），写入基本配置： 

```ini
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录
basedir=C:\Program Files\MySQL
# 设置mysql数据库的数据的存放目录
datadir=C:\Program Files\MySQL\Data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 默认使用“mysql_native_password”插件认证
#mysql_native_password
default_authentication_plugin=mysql_native_password
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8

```

### 2. 安装

- **在安装时，尽量用管理员身份运行CMD，否则在安装时会报错，会导致安装失败的情况**
- 进入MySQL文件夹，**在MySQL的安装目录的仓目录下执行命令：**

```bash
mysqld --initialize --console
```

![04_MySQL安装](/应用使用总结/image/04_MySQL安装.png)

> 注意 [MY-010454]为root @ localhost生成临时密码：`TgyLiu-N:6++`其中root @ localhost：后面的TgyLiu-N:6++就是初始密码（不含首位空格）。
>
> 在没有更改密码前，需要记住这个密码，后续登录需要用到。


- 安装服务

> **在C：\ Windows \ System32目录下找到cmd.exe右键以管理员身份运行**；
>
> CD进入的MySQL的仓目录**下执行命令：**
>
> ```bash
>  mysqld --install [服务名]（服务名可以不加,默认为mysql）
> ```
>
> 出现提示`Service successfully installed`则表示安装成功
>
> > 如果出现`The Service already exists!`,则说明该mysql服务存在，可以将其删掉了。可执行下面的命令将其删掉：
> >
> > ```bash
> > sc delete mysql
> > ```
> > 删掉之后再重新执行上面的安装服务。

- 服务安装成功之后通过命令,启动MySQL的服务:
```bash
net start mysql
```

---
至此 MySQL服务启动成功

## SQLyog

### 1. 使用SQLyog链接mysql服务

![05_MySQL连接](/应用使用总结/image/05_MySQL连接.png)

### 2. 修改root用户密码

```sql
mysqladmin -u root -p 原密码 password 新密码 
```

