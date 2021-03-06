# 前言

命令行小工具

```bash
apt install neofetch
```



系统软件更新

```bash
apt update
apt list —upgradable
```

```zsh
sudo apt update&& sudo apt upgrade
```

```shell
# alias
nano ~/.bashrc
source ~/.bashrc
```



#  1. 软件安装

## apt-get安装

apt-get是Debian系统下进行软件管理的工具，可以安装和卸载软件包。

* 安装软件 

  ```shell
   apt-get install softname
  ```

* 删除软件包，但是不删除软件的配置文件：

  ```shell
  apt-get remove softname
  ```

  如果再想安装，可能会出现问题。

* 删除软件包，并删除相应的配置文件：

  ```shell
  apt-get remove --purge softname 
  ```

*  将依赖的软件包卸载掉，这样就可以完全卸载一个软件。

  ```shell
  apt-get autoremove softname
  ```
  
* 检查是否卸载完成

  ```shell
  softname -V
  ```

* 更新软件信息数据库 

  ```shell
  apt-get update
  ```

* 进行系统升级

  ```shell
  apt-get upgrade 
  ```

* 搜索软件包： 

  ```shell 
  apt-cache search 
  ```



## deb安装



Deb软件包相关安装与卸载

* 安装deb软件包

  ```shell 
  dpkg -i xxx.deb
  ```

* 删除软件包

  ```shell
  dpkg -r xxx.deb
  ```

* 连同配置文件一起删除

  ```shell
  dpkg -r --purge xxx.deb
  ```

* 查看软件包信息

  ```shell
  dpkg -info xxx.deb
  ```

* 查看文件拷贝详情

  ```she
  dpkg -L xxx.deb
  ```

* 查看系统中已安装软件包信息

  ```shell
  dpkg -l
  ```






# 2. 压缩&解压



## unzip



安装unzip

```shell
sudo apt install unzip
```

解压

```shell
unzip latest.zip
```

静默运行

```shell
unzip -q filename.zip
```

解压到另一个目录

```shell
unzip filename.zip -d /path/to/directory
```

解压密码保护的zip

```shell
unzip -P Password filename.zip
```


解压缩 `ZIP` 文件时排除文件

```shell
unzip filename.zip -x file1-to-exclude file2-to-exclude
```

> 示例：将从 `ZIP` 归档文件中提取除. git 目录以外的所有文件和目录

```shell
unzip filename.zip -x "*.git/*"
```

覆盖现有文件：执行相同命令

```shell
unzip latest.zip
```

没有提示的情况下覆盖现有文件，请使用-o 选项

```shell
unzip -o filename.zip
```

解压zip文件而不改写现有文件：保留更改且还原删除的文件

```shell
unzip -n filename.zip
```

解压多个文件

```shell
unzip '*.zip'
```

列出zip文件的内容

```shell
unzip -l filename.zip
```



## tar



tar [必要参数] [可选参数] [文件]

tar本身不具有压缩功能。他是调用压缩功能实现的

| 参数 | 功能                                              |
| ---- | ------------------------------------------------- |
| -c   | （create）建立压缩档案---表示生成新的包           |
| -x   | 解压---解压包                                     |
| -t   | (tarfile)查看内容---查看压缩包的内容              |
| -r   | 向压缩归档文件末尾追加文件---往压缩包里面添加文件 |
| -u   | （update）更新原压缩包中的文件---更新包里的文件   |

| 参数 | 功能                                                         |
| ---- | ------------------------------------------------------------ |
| -z   | 有gzip属性的                                                 |
| -j   | 有bz2属性的                                                  |
| -Z   | 有compress属性的                                             |
| -v   | 显示所有过程                                                 |
| -O   | 将文件解开到标准输出                                         |
| -f   | 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名 |



将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包，-f指定包的文件名

```shell
tar -cf all.tar *.jpg 
```

将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思

```shell
tar -rf all.tar *.gif
```

这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思

```shell 
tar -uf all.tar logo.gif
```

这条命令是列出all.tar包中所有文件，-t是列出文件的意思

```shell
tar -tf all.tar
```

这条命令是解出all.tar包中所有文件，-x是解开的意思

```shell 
tar -xf all.tar 
```

在不解压的情况下查看压缩包的内容

```shell 
tar -tf aaa.tar.gz 
```



压缩

将目录里所有jpg文件打包成jpg.tar

```shell
tar –cvf jpg.tar *.jpg 
```

将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz

```shell
tar –czf jpg.tar.gz *.jpg
```

将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2

```shell
tar –cjf jpg.tar.bz2 *.jpg
```

将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z

```shell
tar –cZf jpg.tar.Z *.jpg
```



解压 tar包

```shell
tar –xvf file.tar
```

解压tar.gz

```shell
tar -xzvf file.tar.gz
```

解压 tar.bz2

```shell
tar -xjvf file.tar.bz2 
```

解压tar.Z

```sh
tar –xZvf file.tar.Z 
```



总结

```shell
1、*.tar 用 tar –xvf 解压

2、*.gz 用 gzip -d或者gunzip 解压

3、*.tar.gz和*.tgz 用 tar –xzf 解压

4、*.bz2 用 bzip2 -d或者用bunzip2 解压

5、*.tar.bz2用tar –xjf 解压

6、*.Z 用 uncompress 解压

7、*.tar.Z 用tar –xZf 解压
8、*.tar.xz 用tar -xJf解压
```





# 3.删除

使用删除文件 rm
要从命令行中删除（或删除）Linux中的文件，请使用rm（删除）。最简单的情况是删除当前目录中的单个文件。键入rm命令，空格，然后输入要删除的文件的名称：

```shell
rm file.txt
```



您可以将多个文件名传递给rm。这样做会删除所有指定的文件：

```shell
rm file_1.txt file_2.txt
```



使用删除目录 rm
要删除空目录，请使用-d （目录）选项。您可以*在目录名称中使用通配符（），就像在文件名中一样：

```shell
rm -d directory
```




一个以上的目录名称将删除所有指定的空目录：

```shell
rm -d directory directory1 /path/to/directory2
```


要删除不为空的目录并取消显示这些提示，请一起使用-r（递归）和-f（强制）选项：

```shell
rm -rf directory
```


使用删除目录 rmdir
在Linux中，您可以使用rmdir和删除目录rm。rm和之间的区别rmdir是rmdir只能删除空目录。它永远不会删除文件。
删除当前目录中的单个目录：



```shell
rmdir directory
```


删除多个目录：

```shell
rmdir directory1 directory2 directory3
```


通过指定该目录的完整路径来删除不在当前目录中的目录：

```shell
rmdir /path/to/directory
```



#  4. 远程手机设备

安装

```shell
#install
#scrcpy
apt install scrcpy
#adb
apt install android-platform-tools
```

连接

```shell
adb tcpip 5555
adb connect 192.168.1.xx:5555
scrcpy
```









# 5.服务器端口

刚刚接触服务器踩的坑，以下适合Linux Bebian10操作系统的服务器，开启防火墙以及端口持久化的方法

如果遇到创建服务器的时候报错服务器错误，或者点击日志发现主机拒绝访问这种情况可能是服务器的防火墙没有开启

排查方法：

```bash
sudo netstat -tlpn
```

```bash
telnet：prot
```

 看是否可以连通

如果没法连通需要开放防火墙端口 

首先安装 iptables（通常系统都会自带，如果没有就需要安装），使用以下命令 

```zsh
sudo apt-get update 

sudo apt-get install iptables 
```

安装成功后使用以下命令开放一个个端口 

```bash
iptables -I INPUT -p tcp --dport 8080 -j ACCEPT 
```

开启一个范围的端口

```bash
iptables  -A INPUT -p tcp --dport 51000：60000 -j ACCEPT
```



设置完就已经放行了指定的端口，但重启后会失效，所以需要设置持续生效规则： 

输入以下安装 iptables-persistent 

```bash
sudo apt-get install iptables-persistent 
```

输入以下命令保存规则持续生效 

```bash
netfilter-persistent save 
netfilter-persistent reload 
```

完成之后端口就会持续开放。



**netstat**

```bash
netstat -tunlp  #用于显示 tcp，udp 的端口和进程等相关情况。
```

netstat 查看端口占用语法格式：

```bash
netstat -tunlp | grep 端口号
```

| 选项     | 功能                                     |
| -------- | ---------------------------------------- |
| -t (tcp) | 仅显示tcp相关选项                        |
| -u (udp) | 仅显示udp相关选项                        |
| -n       | 拒绝显示别名，能显示数字的全部转化为数字 |
| -l       | 仅列出在Listen(监听)的服务状态           |
| -p       | 显示建立相关链接的程序名                 |



例如查看 8000 端口的情况，使用以下命令：

```bash
netstat -tunlp | grep 8000
```

```bash
tcp 0 0 0.0.0.0:8000 0.0.0.0:* LISTEN 26993/nodejs
```



更多命令：

```bash
# 查看当前所有tcp端口
netstat -ntlp 

#查看所有80端口使用情况
netstat -ntulp | grep 80

# 查看所有3306端口使用情况
netstat -ntulp | grep 3306
```

**kill**

在查到端口占用的进程后，如果你要杀掉对应的进程可以使用 kill 命令：

```bash
kill -9 PID
```

如上实例，我们看到 8000 端口对应的 PID 为 26993，使用以下命令杀死进程：

```bash
kill -9 26993
```

# 6.基本环境配置

```bash
apt-get install bash-completion

apt install build-essential
```



## /etc/sudoers

```
:~# nano /etc/sudoers
```

The file does not have too many lines. In the user privilege specification section, you will find a line like this.

```
root ALL=(ALL:ALL) ALL
```

Under it, add your user and leave the rest the same. Something like that.

```
your-user ALL=(ALL:ALL) ALL
```



# 7.shell



## 1.Login  Non-Login Shell

[What is a Shell in UNIX-Based Systems](https://www.delftstack.com/howto/linux/difference-between-a-login-shell-and-a-non-login-shell/#what-is-a-shell-in-unix-based-systems)

A shell in UNIX-based systems is an interface between the user and the operating system’s kernel. It takes input from the user and sends it to the kernel, and it also takes the result from the kernel to the user.

There are two types of shells, the login shell and the non-login shell.

Every shell executes a series of start-up scripts to set up the environment once it is started. The scripts have different uses, and they all affect the environment.

Subsequent scripts can override the values that the previous scripts have set up.

[What is a Login Shell in UNIX-Based Systems](https://www.delftstack.com/howto/linux/difference-between-a-login-shell-and-a-non-login-shell/#what-is-a-login-shell-in-unix-based-systems)

A login shell is the first process that is started after successfully logging in using `/bin/login` by reading the `/etc/passwd` file. The login shell executes under your user ID.

A login shell is executed when you log in using the terminal, switch to another user, or use SSH.

Once a login shell is started, it executes a collection of start-up scripts to set up the shell environment. The following scripts are executed.

1. The login process executes `/etc/profile`.
2. `/etc/profile` executes the scripts in `/etc/profile.d`
3. Login process executes `~/.bash_profile`.
4. `~/.bash_profile` executes `~/.bashrc`
5. `~/.bashrc` executes `/etc/bashrc`

The following command is used to indicate if the shell is a login shell or not.

```bash
echo  $0
```

Getting `-bash` or `-su` as the output indicates that the shell is a login shell. Take note of the `-` symbol preceding the output.

In the image below, the output of the `echo $0` command has a `-` preceding the `bash`. It shows that the shell is a login shell.

![login shell](https://www.delftstack.com/ezoimgfmt/d33wubrfki0l68.cloudfront.net/bd859d144c0037f4beb72a1cd4b91708f6a17029/e6945/img/linux/login_shell.png?ezimgfmt=rs:274x35/rscb5/ng:webp/ngcb5)

[What is a Non-Login Shell in UNIX-Based Systems](https://www.delftstack.com/howto/linux/difference-between-a-login-shell-and-a-non-login-shell/#what-is-a-non-login-shell-in-unix-based-systems)

The login shell starts a non-login shell. It can be a shell that starts with a process without login or starts from another shell. A process uses the name of the shell executable to start a non-login shell.

Running the bash shell as a non-login shell executes the following scripts.

1. Non-login process executes `~/.bashrc`
2. `~/.bashrc` executes `/etc/bashrc`
3. `/etc/bashrc` executes `/etc/profile.d/`

To determine if a shell is a non-login shell or not, run the following command.

```bash
echo $0
```

If the output is `bash` or `su` without a preceding `-` symbol, the shell is a non-login shell.

We execute the `echo $0` command in the image below, and the output shows a `-` preceding the `bash`. It means that we are using a login shell.

To start a non-login shell, we type the name of the shell executable, `bash`, in our case. We execute the `echo $0` command again to see what type of shell the newly started shell is; the output of the `echo` command is `bash` without the `-`. It means the new shell is a non-login shell.

![nonlogin shell](https://www.delftstack.com/ezoimgfmt/d33wubrfki0l68.cloudfront.net/91040ed8e4b1074ed69200b337b1b3f37fabe99f/2b1cc/img/linux/nonlogin_shell.png?ezimgfmt=rs:268x99/rscb5/ng:webp/ngcb5)









## 2.Shell Scripting – Interactive and Non-Interactive Shell

- Last Updated : 27 Jan, 2022

A shell gives us an interface to the Unix system. While using an operating system, we indirectly interact with the shell. On Linux distribution systems, each time we use a terminal, we interact with the shell. The job of the shell is to interpret or analyze the Unix commands given by users. A shell accepts commands from the user and transforms them into a form that is understandable to the kernel. In other words, it acts as a mediator between ta user and the kernel unit of the operating system.

Some of the features of a shell are listed below:

- Wildcard substitution in file names (pattern-matching)
- Command history
- Filename substitution
- Piping

This article focuses upon the interactive and non-interactive shell.

### Interactive shell:

An interactive shell is defined as the shell that simply takes commands as input on tty from the user and acknowledges the output to the user. This shell also reads startup files that occurred during activation and displays a prompt. It also enables job control by default. It is also clear from the name, it is a shell with which we can interact. An interactive script is a script that requires input from the user. Interactive scripts couldn’t run in the background as they required input from the user. For an interactive shell, the prompt variable necessarily is set to ($PS1).

For example, a bash shell is an interactive shell. 

### How to start an interactive shell?

We can start an interactive shell by giving the name of the shell after we logged into the system.

For example,

```
bash
```

This will start bash shell.

### Non-interactive shell:

As the name implies, a non-interactive shell is a type of shell that doesn’t interact with the user. We can run it through a script or similar. Also, it can be run through some automated process. In this case  .bashrc and .profile files do not get executed. The non-interactive shell influences the PATH variable. It is highly recommended to use the full path for a command in non-interactive shells. Non-interactive scripts can smoothly run in the background easily. This shell is generally a non-login shell because the calling user has logged in already. A shell that runs a script is always considered a non-interactive shell.

Scripts like Init and startup are considered non-interactive since they must run without human intervention.

### How to check which type of shell is being used?

The type of shell being used can be detected (BASH only). We can determine if we are using an interactive or non-interactive shell by,

> [[ $- == *i* ]] && echo ‘Interactive’ || echo ‘not-interactive’

