# sudoers的配置

原文：[https://blog.csdn.net/yehongfeiaaa/article/details/8245694]

----

`sudoers` 是 `sudo` 的主要配置文件, linux 下通常在 `/etc` 目录下，如果是 solaris，缺省不装 `sudo` 的，编译安装后通常在安装目录的 `etc` 目录下，不过不管 `sudoers` 文件在哪儿，`sudo` 都提供了一个编辑该文件的命令：`visudo` 来对该文件进行修改。强烈推荐使用该命令修改 `sudoers`，因为它会帮你校验文件配置是否正确，如果不正确，在保存退出时就会提示你哪段配置出错的。

言归正传，下面介绍如何配置 `sudoers`

首先写 `sudoers` 的缺省配置：

```
#############################################################
# sudoers file.
#
# This file MUST be edited with the 'visudo' command as root.
#
# See the sudoers man page for the details on how to write a sudoers file.
#
# Host alias specification
# User alias specification
# Cmnd alias specification
# Defaults specification
# User privilege specification
root ALL=(ALL) ALL
# Uncomment to allow people in group wheel to run all commands
# %wheel ALL=(ALL) ALL
# Same thing without a password
# %wheel ALL=(ALL) NOPASSWD: ALL
# Samples
# %users ALL=/sbin/mount /cdrom,/sbin/umount /cdrom
# %users localhost=/sbin/shutdown -h now
##################################################################
```

## 1. 最简单的配置，让普通用户 `support` 具有 `root` 的所有权限

执行 `visudo` 之后，可以看见缺省只有一条配置：

```
root ALL=(ALL) ALL
```

那么你就在下边再加一条配置：

```
support ALL=(ALL) ALL
```

这样，普通用户 `support` 就能够执行 `root` 权限的所有命令。

以 `support` 用户登录之后，执行：

```
sudo su -
```

然后输入 `support` 用户自己的密码，就可以切换成 `root` 用户了。

## 2. 让普通用户 `support` 只能在某几台服务器上，执行 `root` 能执行的某些命令

首先需要配置一些 Alias，这样在下面配置权限时，会方便一些，不用写大段大段的配置。

Alias 主要分成4种：**Host_Alias**, **Cmnd_Alias**,**User_Alias**,**Runas_Alias**

1) 配置 **Host_Alias**：就是主机的列表

    ```
    Host_Alias HOST_FLAG = hostname1, hostname2, hostname3
    ```

2) 配置 **Cmnd_Alias**：就是允许执行的命令的列表，命令前加上!表示不能执行此命令.

    命令一定要使用绝对路径，避免其他目录的同名命令被执行，造成安全隐患 ,因此使用的时候也是使用绝对路径!

    ```
    Cmnd_Alias COMMAND_FLAG = command1, command2, command3 ，!command4
    ```

3) 配置 **User_Alias**：就是具有 `sudo` 权限的用户的列表

    ```
    User_Alias      USER_FLAG = user1, user2, user3
    ```

4) 配置 **Runas_Alias**：就是用户以什么身份执行（例如 `root`，或者 `oracle`）的列表

    ```
    Runas_Alias     RUNAS_FLAG = operator1, operator2, operator3
    ```

5) 配置权限

    配置权限的格式如下：

    ```
    USER_FLAG HOST_FLAG=(RUNAS_FLAG) COMMAND_FLAG
    ```

    如果不需要密码验证的话，则按照这样的格式来配置：

    ```
    USER_FLAG HOST_FLAG=(RUNAS_FLAG) NOPASSWD: COMMAND_FLAG
    ```

**配置示例**：

```
############################################################################
# sudoers file.
#
# This file MUST be edited with the 'visudo' command as root.
#
# See the sudoers man page for the details on how to write a sudoers file.
#
# Host alias specification
Host_Alias EPG = 192.168.1.1, 192.168.1.2
# User alias specification
# Cmnd alias specification
Cmnd_Alias SQUID = /opt/vtbin/squid_refresh, !/sbin/service, /bin/rm

Cmnd_Alias ADMPW = /usr/bin/passwd [A-Za-z]*, !/usr/bin/passwd, !/usr/bin/passwd root
# Defaults specification
# User privilege specification
root ALL=(ALL) ALL
support EPG=(ALL) NOPASSWD: SQUID
support EPG=(ALL) NOPASSWD: ADMPW
# Uncomment to allow people in group wheel to run all commands
# %wheel ALL=(ALL) ALL
# Same thing without a password
# %wheel ALL=(ALL) NOPASSWD: ALL
# Samples
# %users ALL=/sbin/mount /cdrom,/sbin/umount /cdrom
# %users localhost=/sbin/shutdown -h now
###############################################################
```

---------------------

本文来自 yehongfeiaaa 的CSDN 博客 ，全文地址请点击：https://blog.csdn.net/yehongfeiaaa/article/details/8245694?utm_source=copy