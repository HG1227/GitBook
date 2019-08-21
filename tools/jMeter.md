### 课堂笔记

Postman接口测试\(有chorm的插件\)

录制接口\(查看有哪些接口\)

Navicat\(单一的针对数据库进行可视化\)可视化数据库\(类似于Xampp\)

Jmeter\(后台\)

基于Java的web应用压力测试，后转型成http、ftp服务器等进行压力测试、接口测试

# jMeter {#95-jmeter}

## 一、JMeter之HTTP协议接口性能测试 {#一、jmeter之http协议接口性能测试}

### 1.HTTP基础知识 {#1http基础知识}

#### 1.1 不同角色眼中的接口 {#11-不同角色眼中的接口}

1. 开发眼中的接口 测试眼中的接口
2. 开发眼中的接口：模块与模块之间的对接方式定义
3. 测试眼中的接口：协议接口，可以独立部署成服务的协议接口

#### 1.2 常见的接口协议 {#12-常见的接口协议}

1. HTTP 超文本传输协议
2. HTTPS 安全超文本传输协议
3. FTP 文件传输协议
4. TCP 网络控制协议
5. IP 互联网协议
6. UDP 用户数据协议

#### 1.3 HTTP协议栈中的位置 {#13-http协议栈中的位置}

![](https://hxgqh.gitbooks.io/testautomization/content/assets/guan1.png)

#### 详细：[http://blog.csdn.net/xw20084898/article/details/39438783](http://blog.csdn.net/xw20084898/article/details/39438783) {#详细：httpblogcsdnnetxw20084898articledetails39438783}

#### 1.4 HTTP协议响应码 {#14-http协议响应码}

1. 1xx信息响应类，表示接收到请求并且继续处理
2. 2xx处理成功响应类，表示动作被成功接收、理解和接受
3. 3xx重定向响应类，为了完成指定动作，必须接受进一步处理
4. 4xx客户端错误，客户请求包含语法错误或者不能正确执行
5. 5XX服务端错误，服务器不能正确执行一个正确请求

#### 1.5 客户端-&gt;api-&gt;DB-&gt;api-&gt;客户端 {#15-客户端-api-db-api-客户端}

### 二、JMeter {#二、jmeter}

#### 1 JMeter介绍 {#1-jmeter介绍}

```
    Apache JMeter是Apache组织开发的基于Java的压力测试工具。用于对软件做压力测试，它最初被设计用于Web应用测试，但后来扩展到其他测试领域。 它可以用于测试静态和动态资源，例如静态文件、Java 小服务程序、CGI 脚本、Java 对象、数据库、FTP 服务器， 等等。JMeter 可以用于对服务器、网络或对象模拟巨大的负载，来自不同压力类别下测试它们的强度和分析整体性能。另外，JMeter能够对应用程序做功能/回归测试，通过创建带有断言的脚本来验证你的程序返回了你期望的结果。为了最大限度的灵活性，JMeter允许使用正则表达式创建断言。

  Apache jmeter 可以用于对静态的和动态的资源（文件，Servlet，Perl脚本，java 对象，数据库和查询，FTP服务器等等）的性能进行测试。它可以用于对服务器、网络或对象模拟繁重的负载来测试它们的强度或分析不同压力类型下的整体性能。你可以使用它做性能的图形分析或在大并发负载测试你的服务器/脚本/对象。

```

#### 2.JMeter的优缺点 {#2jmeter的优缺点}

利用Jmeter做功能测试有以下优点：

Ø 不依赖于界面，如果服务正常启动，传递参数明确就可以添加测试用例，执行测试

Ø 测试脚本不需要编程，熟悉http请求，熟悉业务流程，就可以根据页面中input对象来编写测试用例。

Ø 测试脚本维护方便，可以将测试脚本复制，并且可以将某一部分单独保存。

Ø 可以跳过页面限制，向后台程序添加非法数据，这样可以测试后台程序的健壮性。

Ø 利用badboy录制测试脚本，可以快速的形成测试脚本

Ø Jmeter断言可以验证代码中是否有需要得到的值

Ø 使用参数化以及Jmeter提供的函数功能，可以快速完成测试数据的添加修改等

利用Jmeter做功能测试有以下缺点：

Ø 使用Jmeter无法验证JS程序，也无法验证页面，所以需要手工去验证。

Ø Jmeter的断言功能不是很强大

Ø 就算是jmeter脚本顺利执行，依旧无法确定程序是否正确执行，有时候需要进入程序查看，或者查看Jmeter的响应数据。

Ø Jmeter脚本的维护需要保存为本地文件，而每个脚本文件只能保存一个测试用例，不利于脚本的维护。

Jmeter和其他功能测试工具在使用中的比较：

Ø Jmeter比较适用于数据添加，数据修改，数据查询的测试，使用其他测试工具虽然也可以完成该类测试，但是利用Jmeter添加数据更快，更方便，而且不依赖于界面，只要添加数据的参数不改变，无论界面是否有变动，都不影响针对数据的操作。

Ø Jmeter不需要要关注对象是否被识别的问题，而其他测试工具在录制过程中，很容易出现页面对象不能被录制工具识别的问题，因此适用Jmeter，省略了很多关于对象操作的麻烦，更易于使用。

Ø Jmeter的适用更主要的是依赖于对被测项目的认知和熟悉，而对于Jmeter自身的适用技巧要求并不是很高，而其他测试工具，关于工具本身需要较长时间的学习。

Ø Jmeter能够对复杂的业务逻辑进行处理，而对这些复杂业务逻辑的处理，主要是运用Jmeter自身所带的配置元件来达到，对录制的脚本的修改不大，而 使用其他测试工具，要实现复杂业务逻辑的测试，则需要对录制的脚本进行修改，需要工具使用人员有一点的编程能了，因此，使用Jmeter进行测试对测试人 员编程能力的要求不高，同时节省大量的修改脚本的时间。

Ø 其他测试工具的测试脚本可以通过CVS等版本控制工具进行管理，而Jmeter的测试脚本的管理不知道是否可以纳入版本控制，因此，其他测试工具比较适用 于大型的，系统的功能测试中，而Jmeter比较适用于随机的，扩展开发不多的项目，也就是说Jmeter使用起来更灵活。

Ø 其他测试工具有大量的验证点可用，并且能够对界面上的内容进行验证，可以验证更多的内容，测试能够更完全，对于界面变动不大的项目，可以通过修改脚本实现 更加全面的自动化测试，而Jmeter提供的断言功能有限，并且不依赖于界面，无法完界面相关内容的验证，用Jmeter测试更需要人工测试，人工确认。

Ø Jmeter用作一个辅助测试工具，可以很大的提高测试人员的效率，而其他测试工具当作辅助测试工具并不能达到和jmeter同样的功能。

Ø Jmeter做功能测试的脚本可以同样用来做性能测试，这是其他大多数功能测试工具所不能具备的。

# JMeter数据库测试计划 {#jmeter数据库测试计划--jmeter教程}

在本章中，我们将看到如何创建一个简单的测试计划，测试数据库服务器。对于我们的测试目的，我们使用MySQL数据库服务器。您可以使用任何其他数据库进行测试。MYSQ的安装和创建表，请参阅[MYSQL教程](http://www.yiibai.com/mysql/index.html)。

安装MySQL以后，请按照以下步骤设置数据库：

* 创建一个数据库名称 "tutorial".

* 创建一个表 tutorials\_tbl.

* 插入记录到 tutorials\_tbl :

  ```
  mysql

  &

  gt; use TUTORIALS;
  Database changed
  mysql

  &

  gt; INSERT INTO tutorials_tbl 
       -

  &

  gt;(tutorial_title, tutorial_author, submission_date)
       -

  &

  gt;VALUES
       -

  &

  gt;("Learn PHP", "John Poul", NOW());
  Query OK, 1 row affected (0.01 sec)
  mysql

  &

  gt; INSERT INTO tutorials_tbl
       -

  &

  gt;(tutorial_title, tutorial_author, submission_date)
       -

  &

  gt;VALUES
       -

  &

  gt;("Learn MySQL", "Abdul S", NOW());
  Query OK, 1 row affected (0.01 sec)
  mysql

  &

  gt; INSERT INTO tutorials_tbl
       -

  &

  gt;(tutorial_title, tutorial_author, submission_date)
       -

  &

  gt;VALUES
       -

  &

  gt;("JAVA Tutorial", "Sanjay", '2007-05-06');
  Query OK, 1 row affected (0.01 sec)
  mysql

  &

  gt;

  ```

* 复制JDBC驱动程序到 /home/manisha/apache-jmeter-2.9/lib.

## 创建JMeter测试计划 {#创建jmeter测试计划}

首先，让我们启动JMeter /home/manisha/apache-jmeter-2.9/bin/jmeter.sh.

### 添加用户 {#添加用户}

现在，创建一个线程组，右键点击 Test Plan &gt; Add&gt; Threads\(Users\)&gt; Thread Group. 根据测试计划节点将添加线程组。重命名此线程为JDBC用户。

![](https://wizardforcel.gitbooks.io/tutorialspoint-java/content/img/2154101338-0.jpg)

我们不会改变线程组的默认属性。

### 添加JDBC请求 {#添加jdbc请求}

现在，我们已经定义了我们的用户，它是时间来定义，他们将要执行的任务。在本节中将指定JDBC请求执行。 JDBC Users元件上右击，选择 Add &gt; Config Element &gt; JDBC Connection Configuration.

设置以下字段（我们使用的是MySQL数据库教程）：

* 变量名绑定到池。这需要唯一地标识该配置。它是用来由JDBC采样器，以确定要使用的配置。作为测试，我们把它命名为 test

* Database URL: jdbc:mysql://localhost:3306/tutorial

* JDBC Driver class: com.mysql.jdbc.Driver

* 用户名: root

* 密码: root的密码

在屏幕上的其他领域，可以留为默认值，如下所示：

![](https://wizardforcel.gitbooks.io/tutorialspoint-java/content/img/21541055I-1.jpg)

添加一个JDBC请求是指上面定义的JDBC配置池。选择JDBC Users元件，单击鼠标右键得到添加菜单，然后选择 Add &gt; Sampler &gt; JDBC Request. 然后，选择这个新的元素，以查看它的控制面板。编辑属性如下：

* 变量名绑定到池。这需要唯一地标识该配置。它是用来由JDBC采样器，以确定要使用的配置。我们将其命名为 test

* Name: Learn

* Enter the Pool Name: test \(same as in the configuration element\)

* Query Type: Select statement

* Enter the SQL Query String field.

![](https://wizardforcel.gitbooks.io/tutorialspoint-java/content/img/2154101952-2.jpg)

### 创建侦听器 {#创建侦听器}

现在添加Listener元素。此元素负责存储所有JDBC请求的结果，在一个文件中，并呈现出可视化的数据模型。

选择JDBC Users元件，并添加一个查看结果树监听器\(Add &gt; Listener &gt; View Results Tree\).

![](https://wizardforcel.gitbooks.io/tutorialspoint-java/content/img/2154104Q8-3.jpg)

### 保存并执行测试计划 {#保存并执行测试计划}

现在保存的以上测试计划db\_test.jmx。执行本测试计划使用 Run &gt; Start 选项.

### 校验输出 {#校验输出}

![](https://wizardforcel.gitbooks.io/tutorialspoint-java/content/img/2154103T1-4.jpg)![](https://wizardforcel.gitbooks.io/tutorialspoint-java/content/img/2154106155-5.jpg)![](https://wizardforcel.gitbooks.io/tutorialspoint-java/content/img/2154101024-6.jpg)

在最后图像，可以看到，2条记录被选择。

