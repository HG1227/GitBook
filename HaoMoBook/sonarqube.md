# sonarqube {#sonarqube}

## 第一章 SonarQube简介 {#第一章-sonarqube简介}

### 1.1 SonarQube介绍 {#11-sonarqube介绍}

Sonar 是一个用于代码质量管理的开源平台，用于管理源代码的质量

通过插件形式，可以支持包括 java,C\#,C/C++,PL/SQL,Cobol,JavaScrip,Groovy,HTML,Python,PHP,XML等等二十几种编程语言的代码质量管理与检测

Sonar可以从以下七个维度检测代码质量

1. 不遵循代码标准 sonar可以通过PMD,CheckStyle,Findbugs等等代码规则检测工具规 范代码编写
2. 潜在的缺陷 sonar可以通过PMD,CheckStyle,Findbugs等等代码规则检测工具检 测出潜在的缺陷
3. 糟糕的复杂度分布 文件、类、方法等，如果复杂度过高将难以改变，这会使得开发人员 难以理解它们 且如果没有自动化的单元测试，对于程序中的任何组件的改变都将可能导致需要全面的回归测试
4. 重复 显然程序中包含大量复制粘贴的代码是质量低下的，sonar可以展示 源码中重复严重的地方
5. 注释不足或者过多 没有注释将使代码可读性变差，特别是当不可避免地出现人员变动 时，程序的可读性将大幅下降 而过多的注释又会使得开发人员将精力过多地花费在阅读注释上，亦违背初衷
6. 缺乏单元测试 sonar可以很方便地统计并展示单元测试覆盖率
7. 糟糕的设计

## 第二章 SonarQube的安装使用 {#第二章-sonarqube的安装使用}

### 2.1 SonarQube的下载 {#21-sonarqube的下载}

1.SonarQube服务端下载地址：[https://www.sonarqube.org/downloads/；](https://www.sonarqube.org/downloads/%EF%BC%9B)![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Sonarqube1.jpeg)文件下载完成后将文件解压到usr/local目录下，解压后的目录结构如下：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Sonarqube2.jpeg)

2.SonarQube客户端工具下载：[http://repo1.maven.org/maven2/org/codehaus/sonar/runner/sonar-runner-dist/2.4/sonar-runner-dist-2.4.zip](http://repo1.maven.org/maven2/org/codehaus/sonar/runner/sonar-runner-dist/2.4/sonar-runner-dist-2.4.zip)![](https://hxgqh.gitbooks.io/haomotraining/content/assets/sonarqube3.jpeg)文件下载完成后将文件解压到usr/local目录下，解压后的目录结构如下：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Sonarqube4.jpeg)

3.中文补丁包下载地址：[https://github.com/SonarQubeCommunity/sonar-l10n-zh](https://github.com/SonarQubeCommunity/sonar-l10n-zh)

### 2.2SonarQube的环境变量的配置 {#22sonarqube的环境变量的配置}

1.vim ~/.bash\_profile

export SONAR\_HOME=/usr/local/sonarqube-5.6.6

export SONAR\_RUNNER\_HOME=/usr/local/sonar-runner-2.4

export PATH=$PATH:$SONAR\_RUNNER\_HOME/bin:$JAVA\_8\_HOME/bin

配置完成后环境变量生效

source ~/.bash\_profile

试验：sonar-runner -v

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Sonarqube5.jpeg)  
![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Sonarqube6.jpeg)

### 2.3启动SonarQube {#23启动sonarqube}

cd /usr/local/sonarqube-5.6.6/bin/macosx-universal-64

./sonar.sh start

查看启动日志:

tail -f /usr/local/sonarqube-5.6.6/logs/sonar.log

关闭命令:

./sonar.sh stop

登录：[http://localhost:9000/sonarqube](http://localhost:9000/sonarqube)

默认密码:admin/admin

## 第三章 参考资料 {#第三章-参考资料}

1.[http://www.jianshu.com/p/b41262fca5b8](http://www.jianshu.com/p/b41262fca5b8)2.

