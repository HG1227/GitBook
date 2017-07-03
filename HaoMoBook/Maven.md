# Maven培训 {#toc_0}

## 第一章 Maven介绍 {#toc_1}

Maven是Apache组织中的一个很成功的开源项目,主要服务于基于Java平台的项目构建,依赖管理和项目信息管理.

### 1.1 Maven历史 {#toc_2}

Maven的最初设计，以简化Jakarta Turbine项目的构建过程。有几个项目，每个项目包含了稍微不同的Ant构建文件。 JAR中纳入到CVS。

Jakarta Trubine项目有多个工程，每个工程都有自己的多个Ant构建文件。每个工程的这些构建文件都只有一小部分不同，并且所有的Jar文件被使用CVS纳入了版本管理。他们想要实现一种标准方式去构建这些工程、明确定义这些工程的组成部分、简单的发布工程信息以及多个工程间共享Jar包。

就这样，一个能够构建和管理任何基于Java的工程的工具诞生了。

### 1.2 Maven是什么？ {#toc_3}

Maven是一个构建工具、依赖管理工具、项目信息管理工具。

个人理解：构建工具 —— 自动化构建过程。以打包部署为例，经历的过程是 清理 --&gt; 编译 --&gt;测试--&gt;生成报告--&gt;打包部署

依赖管理工具 —— 具体来说,就是它提供了中央仓库,我们可以获得想要的构件,而这些构件也是Maven自动下载的.在我们的项目中,要借用一些第三方的开源类库,这些类库都是通过依赖的方式引入到项目中,但依赖太多就会产生一系列问题,比如,版本不一致,版本冲突,依赖臃肿等.这时,Maven提供了一个特别好的解决方案,它通过一个坐标系统准确的定位一个构件,换句话说就是用一组坐标找到唯一的一个Java类库,借助坐标管理构件让我们的依赖有序了.

管理包括项目描述,开发者列表等信息,帮助我们获得测试报告,日志报告等项目信息.Maven对于项目目录结构和测试用例命名方式等都有既定的规则,遵循这些规则,用户在项目间切换的时候就不用额外的学习成本,这一点可以说是约定优于配置.

```
     Maven是跨平台的,无论是在windows上还是Linux上或者Mac上都能使用同样的命令,它对外提供一致的操作接口,这是它流行的重要原因.

```

### 1.3 Maven目标 {#toc_4}

Maven主要目标是提供给开发人员：

```
项目是可重复使用，易维护，更容易理解的一个综合模型。

插件或交互的工具，这种声明性的模式。

```

### 1.4 Maven基本单元 {#toc_4}

Maven项目的结构和内容在一个XML文件中声明，pom.xml 项目对象模型（POM），这是整个Maven系统的基本单元。

Apache Maven 是一种创新的软件项目管理工具，提供了一个项目对象模型（POM）文件的新概念来管理项目的构建，相关性和文档。最强大的功能就是能够自动下载项目依赖库

### 1.5 Maven优势 {#toc_4}

1.我们一直在寻找避免重复的方法，设计的重复，文档的重复，编码的重复，构建的重复等，最大的消除了构建的重复。

2.maven是跨平台的。

3.maven不仅是构建工具，它还是依赖管理工具和项目管理工具，提供了中央仓库，能够帮我们自动下载构件。

4.为了解决的依赖的增多，版本不一致，版本冲突，依赖臃肿等问题，它通过一个坐标系统来精确地定位每一个构件（artifact）。

5.还能帮助我们分散在各个角落的项目信息，包括项目描述，开发者列表，版本控制系统，许可证，缺陷管理系统地址。

6.maven还为全世界的Java开发者提供了一个免费的中央仓库，在其中几乎可以找到任何的流行开源软件。通过衍生工具\(Nexus\),我们还能对其进行快速搜索。

7.maven对于目录结构有要求，约定优于配置，用户在项目间切换就省去了学习成本。

### 1.6 Maven缺点 {#toc_4}

1. maven是一个庞大的构建系统，学习难度大

2. maven采用约定优于配置的策略（convention over configuration），虽然上手容易，但是一旦出了问题，难于调试。

3. 当依赖很多时，m2eclipse 老是搞得Eclipse很卡。
4. 中国的网络环境差，很多repository无法访问，比如google code， jboss 仓库无法访问等。

## 第二章 Maven安装和配置 {#toc_5}

### 2.1 windows下的安装 {#toc_6}

#### 2.1.1 所需工具 ： {#toc_7}

JDK 1.8 Maven 3.3.3 Windows 7

#### 2.1.2 JDK 和 JAVA\_HOME {#toc_8}

确保已安装JDK，并 “JAVA\_HOME” 变量已加入到 Windows 环境变量。

#### 2.1.3 下载Apache Maven {#toc_9}

下载地址[http://maven.apache.org/download.cgi](http://maven.apache.org/download.cgi)

下载 Maven 的 zip 文件，例如： apache-maven-3.3.3-bin.zip，将它解压到你要安装 Maven 的文件夹。

假设你解压缩到文件夹 – D:\software\yiibai.com\apache-maven 注意：在这一步，只是文件夹和文件，安装不是必需的。

#### 2.1.4 添加 M2\_HOME 和 MAVEN\_HOME {#toc_10}

添加 M2\_HOME 和 MAVEN\_HOME 环境变量到 Windows 环境变量，并将其指向你的 Maven 文件夹。

Maven 说只是添加 M2\_HOME , 但一些项目仍引用 Maven 的文件夹 MAVEN\_HOME, 因此，为了安全也把它添加进去。

#### 2.1.5 添加到环境变量 - PATH {#toc_11}

更新 PATH 变量，添加 Maven bin 文件夹到 PATH 的最后，如： %M2\_HOME%\bin, 这样就可以在命令中的任何目录下运行 Maven 命令了。

#### 2.1.6 验证 {#toc_12}

执行 mvn –version 在命令提示符下

看到 Maven home：路径

说明 Apache Maven 在 Windows 上已安装成功。

## 第三章 Maven资源库 {#toc_13}

### 3.1 Maven本地资源库 {#toc_14}

Maven 的本地资源库是用来存储项目的依赖库，默认的文件夹是 “.m2” 目录，可能需要将其更改为另一个文件夹。

### 3.2 Maven中央存储库 {#toc_15}

Maven 中央存储库是 Maven 用来下载所有项目的依赖库的默认位置\(默认的 Maven 中央存储库[http://repo1.maven.org/maven2/](http://repo1.maven.org/maven/)\)。[http://search.maven.org/](http://search.maven.org/)

### 3.3 如何从Maven远程存储库下载？如何添加远程库？ {#toc_16}

并非所有的库存储在Maven的中央存储库，很多时候需要添加一些远程仓库来从其他位置，而不是默认的中央存储库下载库。

### 3.4 Maven 依赖搜索序列 {#34-maven-依赖搜索序列}

当我们执行 Maven 构建命令，Maven 依赖库按以下顺序进行搜索：

* 第1步 - 搜索依赖本地资源库，如果没有找到，跳到第2步，否则，如果找到那么会做进一步处理。

* 第2步- 搜索依赖中央存储库，如果没有找到，则从远程资源库/存储库中，然后移动到步骤4，否则如果找到，那么它下载到本地存储库中，以备将来参考使用。

* 第3步- 如果没有提到远程仓库，Maven 则会停止处理并抛出错误（找不到依赖库）。

* 第4步 - 远程仓库或储存库中的搜索依赖，如果找到它会下载到本地资源库以供将来参考使用，否则 Maven 停止处理并抛出错误（找不到依赖库）。

### 3.5 Maven依赖机制 {#toc_17}

关于传统方式和Maven方式的依赖库的不同，并说明 Maven 会从那里搜索这些库。

## 第四章 Maven基本操作 {#toc_18}

#### 一些基本的操作，编译，构建，单元测试，安装，网站生成和基于Maven部署项目。 {#toc_19}

```
使用Maven编译项目
“mvn compile” 来构建项目
使用Maven构建项目
  “mvn package” 来构建项目 mvn clean compile package
使用Maven清理项目
  “mvn clean” 来清理项目
使用Maven运行单元测试
  “mvn test” 来执行单元测试
将项目安装到Maven本地资源库
  “mvn install” 打包和部署项目到本地资源库
生成基于Maven的项目文档站点
  “mvn site” 来为您的项目生成信息文档站点
使用“mvn site-deploy”部署站点（WebDAV例子）
  “mvn site-deploy” 通过WebDAV部署自动生成的文档站点到服务器
部署基于Maven的war文件到Tomcat
  “mvn tomcat:deploy” 以 WAR 文件部署到 Tomcat
创建Maven Web项目
mvn archetype:generate -DgroupId=com.haomo. -DartifactId=CounterWebApp  -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false

```

## 第五章 Maven高级操作 {#toc_18}

### 5.1构建Java项目 {#51构建java项目}

mvn archetype:generate -DgroupId={project-packaging} -DartifactId={project-name}-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

### 5.2构建Web项目 {#52构建web项目}

mvn archetype:generate -DgroupId=com.yiibai -DartifactId=CounterWebApp -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false

