# Debain 9

任务：

- 完成操作系统的安装
- 熟悉Unix/Linux常用命令的使用
- 掌握apt工具安装常用软件
- 安装nginx，尝试建立一个web站点



## 关于Debian

### 什么是Debian

Debian 是一个致力于自由软件开发并宣扬自由软件基金会之理念的自愿者组织。Debian 计划创建于 1993 年。当时，Ian Murdock 发出一份公开信，邀请软件开发者们参与构建一个基于较新的 Linux 内核的完整而紧密的软件发行版。经过多年的成长，那群由 [自由软件基金会](http://www.fsf.org/) 资助并受 [GNU](http://www.gnu.org/gnu/the-gnu-project.html) 哲理影响的爱好者已经演变为一个拥有大约 1062 位 *Debian 开发人员的组织*。

Debian 开发人员所做的工作包括有：[Web](http://www.debian.org/) 和 [FTP](ftp://ftp.debian.org/) 站点管理、图形设计、软件许可协议的法律分析、编写文档，当然，还有维护软件包。

### 什么是Debian GNU/Linux

将 Debian 哲学与方法论，GNU 工具集、Linux 内核，以及其他重要的自由软件结合在一起所构成的独特的软件发行版称为 Debian GNU/Linux。

Debian 在高级用户中非常流行的原因在于它具有优秀的技术，而且它对 Linux 的深入贡献满足了社区的需求与期望。Debian 为 Linux 引入的许多特性现在已经成为了非常通用的标准。例如，Debian 是第一种使用包管理系统的 Linux 发行版，它让安装和删除软件变得非常容易。而且它还是第一个可以不用重新安装就能升级的 Linux 发行版。

Debian 与其他 Linux 发行版最大的不同之处在于包管理系统的特性。这些工具给予 Debian 系统管理员对安装到系统上的软件包的完全控制，包括安装单个软件包和自动升级整个操作系统。



## 安装Debian

### 安装环境

虚拟机，VMware Workstation Pro 15，64位PC

### 下载镜像

下载地址，https://cdimage.debian.org/debian-cd/current/amd64/iso-dvd/debian-9.7.0-amd64-DVD-1.iso

使用下载工具进行下载

### 安装镜像

Debian 9支持图形界面安装和字符界面安装两种形式，简易安装教程如下：

- 图形界面，https://jingyan.baidu.com/article/6d704a134fde4c28db51ca8b.html
- 字符界面，https://jingyan.baidu.com/article/d169e18608dd8a436611d82a.html

### 配置系统

- Ctrl + Alt + T 呼出终端
  系统设置 - 键盘 - 添加快捷键，名字：Shell，命令：gnome-terminal，快捷键：Ctrl + Alt + T

- 检查apt源
  采用cdrom安装可能会遗留cdrom在apt源中，导致`apt update`失败
  将`/etc/apt/sources.list`中注释掉下面类似语句

  ```
  #deb cdrom:[Debian GNU/Linux 9.7.0 _Stretch_ - Official amd64 DVD Binary-1 20190123-19:36] stretch contrib main
  ```

  若后续apt安装软件失败，建议换源，在文件中加入下列条目：

  ```
  deb http://mirrors.163.com/debian/ jessie main non-free contrib
  deb http://mirrors.163.com/debian/ jessie-updates main non-free contrib
  deb http://mirrors.163.com/debian/ jessie-backports main non-free contrib
  deb-src http://mirrors.163.com/debian/ jessie main non-free contrib
  deb-src http://mirrors.163.com/debian/ jessie-updates main non-free contrib
  deb-src http://mirrors.163.com/debian/ jessie-backports main non-free contrib
  deb http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib
  deb-src http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib
  ```

  安装vim

  ```shell
  su
  apt install vim
  echo -e "set mouse=i\nsyntax on" > ~/.vimrc
```
  
- 安装sudo

  ```shell
  su
  apt install sudo
  ```

  并将当前用户添加入sudo群组
  在`/etc/sudoers`中，`"Allow members of group sudo to execute any command"`下方添加

  ```
  username ALL=(ALL:ALL) ALL
  ```

  其中username为当前用户名

- 其他

  ```shell
  sudo apt install net-tools 		# netstat
  ```



## Unix/Linux常用命令

| 命令                                                 | 备注                                                         |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| cat *files*                                          | 将多个文件*files*的内容打印到屏幕                            |
| cd *directory*                                       | 改变当前目录至目录*directory*                                |
| cp *file* *dest*                                     | 复制文件*file*到位置*dest*                                   |
| gzip, bzip2, xz [-d] *files*                         | 压缩, 解压缩多个文件*files*                                  |
| pager *files*                                        | 显示多个文件*files*内容                                      |
| ls [*files*]                                         | 列出当前目录下的文件，或列出多个文件*files*                  |
| mkdir *directory-names*                              | 创建多个目录*directory-names*                                |
| mv *file1* *file2*                                   | 移动文件*file1*至文件*file2*，或将文件*file1*重命名为*file2* |
| rm *files*                                           | 删除多个文件*files*                                          |
| rmdir *dirs*                                         | 删除多个空目录*dirs*                                         |
| tar \[c]\[x]\[t]\[z]\[j]\[J] -f *file.tar* [*files*] | 创建[c]，解压缩[x]，列出文件表格[t]，gz格式[z]，bz2格式[j]，xz格式[J] |
| find *directories* *expression*                      | 在*directories*中查找符合*expression*的文件，例如，find -name *name* |
| grep *search-string* *files*                         | 在多个文件*files*中查找指定字符串*search-string*             |
| ln -s *file* *link*                                  | 创建文件*file*的软链接                                       |
| ps [*options*]                                       | 显示当前进程                                                 |
| kill [-9] *PID*                                      | 向进程号为*PID*的进程发送信号，-9为终止信号                  |
| su - [*username*]                                    | 切换至用户*username*                                         |
| sudo *command*                                       | 以root身份执行命令                                           |
| *command* > *file*                                   | 将命令*command*的执行结果覆盖至*file*文件中                  |
| *command* >> *file*                                  | 将命令*command*的执行结果添加至*file*文件中                  |
| *cmd1* \| *cmd2*                                     | 将命令*cmd1*的执行结果作为命令*cmd2*的输入                   |
| *command* < *file*                                   | 将文件*file*的内容作为命名*command*的输入                    |



## APT(Advanced Package Tool)常用命令

| 命令                         | 备注                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| apt update                   | 更新列在/etc/apt/sources.list文件中的软件仓库中的软件包列表信息 |
| apt search *search-string*   | 在软件包名和说明信息中查找字符串search-string                |
| apt list -a *package-name*   | 列出软件包package-name的版本信息                             |
| apt show -a *package-name*   | 显示软件包package-name的详细信息                             |
| apt install *package-names*  | 安装多个软件包package-names及其所需的依赖                    |
| apt upgrade                  | 安装当前已安装所有软件包的最新版本                           |
| apt full-upgrade             | 和apt upgrade类似，但有跟好几的冲突解决方案                  |
| apt remove *package-names*   | 移除多个软件包package-names                                  |
| apt autoremove               | 移除系统中不再被依赖的软件包                                 |
| apt depends *package-name*   | 列出软件包package-name依赖的所有软件包                       |
| apt-file update              | 从软件包升级内容列表，参见apt update                         |
| apt-file search *file-name*  | 在软件包仓库中查找文件file-name                              |
| apt-file list *package-name* | 列出软件包package-name中包含的文件                           |



## 安装Nginx，建立web站点

### 关于Nginx

Nginx是一款自由的、开源的、高性能的HTTP服务器和反向代理服务器；同时也是一个IMAP、POP3、SMTP代理服务器；Nginx可以作为一个HTTP服务器进行网站的发布处理，另外Nginx可以作为反向代理进行负载均衡的实现。

### 安装Nginx

```shell
sudo apt install nginx
```

### 使用Nginx

运行nginx

```shell
sudo systemctl start nginx.service
```

浏览器访问`localhost`，显示`Apache2 Debian Default Page`，则运行成功

停止nginx

```shell
sudo systemctl stop nginx.service
```

### 配置Nginx

Nginx的配置文件为`/etc/nginx/nginx.conf`

文件中包含了对Nginx的默认配置

注释掉`/etc/nginx/nginx.conf`中的下列语句：

```
#include /etc/nginx/conf.d/*.conf;
#include /etc/nginx/sites-enabled/*;
```

新建子配置文件

```
sudo touch /etc/nginx/sites-enabled/demo
```

`/etc/nginx/sites-enabled/demo`文件中定义简单的server块，内容如下：

```
server {
        listen  80;
        listen [::]:80;
        
        server_name example.com;
        
        root /var/www/html;
        index index.nginx-debian.html;
        
        location / {
            try_files $uri $uri/ =404;
        }
}
```

若nginx已运行，更新nginx服务

```
sudo systemctl reload nginx.service
```

浏览器访问`localhost`，显示`Welcome to nginx`，则配置成功



## 参考资料

1. [Debian百度百科](https://baike.baidu.com/item/Debian/748667?fr=aladdin)
2. [Debian GNU/Linux 安装手册](http://www.debian.org/doc/)
3. [debian9安装教程](https://jingyan.baidu.com/article/6d704a134fde4c28db51ca8b.html)
4. [U盘安装debian9.5系统教程](https://jingyan.baidu.com/article/d169e18608dd8a436611d82a.html)
5. [Debian 参考卡片](https://www.debian.org/doc/manuals/refcard/refcard.zh_CN.pdf)
6. [Nginx 相关介绍(Nginx是什么?能干嘛?)](https://www.cnblogs.com/wcwnina/p/8728391.html)
7. [Nginx学习笔记--001-Nginx快速搭建](https://www.cnblogs.com/renjing/p/6126284.html)
8. [如何在Debian 9上安装Nginx](http://linux265.com/news/3367.html)
9. [在Debian上安装Nginx并搭建一个最简单的静态网站服务器](http://ourjs.com/detail/5834f6716345657c15b8db95)
10. [Debian系统下使用自带的Fcitx配置中文输入法](https://blog.csdn.net/wu58430/article/details/81117721)
11. 
