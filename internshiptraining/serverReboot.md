# 项目服务器重启

#### 作者：高天阳
#### 邮箱：gty@haomo-studio.com

```
更改历史

* 2018-2-6  高天阳	初始化文档

```
## 1 简介

项目服务宕掉的时候有时需要重启服务 以下是重启服务的指令

## 2 指令

### 2.1 进入服务器

```angular2html
ssh [服务器地址]
```

```angular2html
➜  ~ ssh member@haomo-tech.com
```

```angular2html
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-62-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

153 个可升级软件包。
60 个安全更新。


  ######################################################################
  #                              Notice                                #
  #                                                                    #
  #  1. Please DO NOT upgrade the kernel, as the kernel upgrade would  #
  #   damage the original operating system.                            #
  #                                                                    #
  #  2. Please create unique passwords that use a combination of words,#
  #   numbers, symbols, and both upper-case and lower-case letters.    #
  #   Avoid using simple adjacent keyboard combinations such as        # 
  #   "Qwert!234","Qaz2wsx",etc.                                       #
  #                                                                    #
  #  3. Unless necessary, please DO NOT open or use high-risk ports,   #
  #   such as Telnet-23, FTP-20/21, NTP-123(UDP), RDP-3389,            #
  #   SSH/SFTP-22, Mysql-3306, SQL-1433,etc.                           #
  #                                                                    #
  #                                                                    #
  #                     Any questions please contact 4000-955-988      #
  ######################################################################
```

### 2.2 进入data目录下

```angular2html
➜  ~ cd /data/
```

### 2.3 查看data文件下内容

```angular2html
➜  ~ ls
```

### 2.4 进入tomcat下的bin目录

```angular2html
➜  ~ cd tomcat/bin
```

### 2.5 执行脚本`./catalina.sh`

```angular2html
➜  ~ ./catalina.sh start
```

```angular2html
./catalina.sh: 249: ./catalina.sh: -Djava.awt.headless=true: not found
Using CATALINA_BASE:   /data/tomcat
Using CATALINA_HOME:   /data/tomcat
Using CATALINA_TMPDIR: /data/tomcat/temp
Using JRE_HOME:        /usr
Using CLASSPATH:       /data/tomcat/bin/bootstrap.jar:/data/tomcat/bin/tomcat-juli.jar
Tomcat started.
```
### 2.6 如果未重启成功 需要先关闭服务再启动

```angular2html
➜  ~ ./catalina.sh stop
```

![](../../assets/serverReboot1.jpeg)
![](../../assets/serverReboot2.jpeg)