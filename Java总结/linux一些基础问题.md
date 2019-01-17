#linux的一些基础问题

### 1. linux的使用场景
> linux是一个长时间运行比较稳定的操作系统，所以我们一般会拿它作为服务器（web，db，APP等）。
> linux本身具有C的编译环境，我们的一些软件是没有软件包（redis等）的，需要在linux的C编译环境编译得到软件包。



### 2. linux的常用命令

- 常用命令：
  - `Pwd` 获取当前路径
  - `Cd` 跳转到目录
  - `Su -u` 切换到管理员、
  - `Ls ls` 列举目录

- 文件操作命令：
  - 文件
    - `Tail` 查看
    - `Rm -rf` 删除
    - `Vi`  修改
  - 文件夹
    - `Mkdir` 创建文件夹
    - `Rm -rf` 删除文件夹

### 3. 怎么连接远程的linux服务器？
> - 需要依赖于linux服务器安装ssh服务端，一般这个ssh服务的端口为22
> - 需要依赖于linux服务器安装sftp服务端，一般这个sftp服务的端口是25
- 使用ssh客户端连接linux服务器，就有点像windows下面的远程连接，但是linux通过ssh连接上以后是没有图形界面，全是命令行。
    putty
    xshell
- 使用sftp客户端来连接sftp服务端，来上传和下载文件。（上传安装包，修改了配置文件上传）
winscp
xftp
- 企业中常用的两种组合：
putty+winscp
xshell+xftp+xmanager

