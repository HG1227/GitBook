# Linux 常用基础命令

1、显示日期的指令： date

![](http://p3.pstatp.com/large/289000006c0de1c05d14 "Linux 常用基础命令")

注意:date 后需要加上时间格式  


2、显示日历的指令：cal

当前月份： cal  


![](http://p3.pstatp.com/large/28860005063fc75cc7f3 "Linux 常用基础命令")

全年月份： eg： cal 2009 为显示2009年全年  


![](http://p3.pstatp.com/large/26f30005001ab5564b8d "Linux 常用基础命令")

指定的年月： eg：cal 10 2009 为2009年10月  


![](http://p1.pstatp.com/large/289000006f2241673827 "Linux 常用基础命令")

3、简单好用的计算器：bc  


![](http://p1.pstatp.com/large/288e0002acbdf241fd1a "Linux 常用基础命令")

注意 ： bc计算器预设只输出整数值  


4、重要的几个热键\[Tab\],\[ctrl\]-c, \[ctrl\]-d

\[Tab\]按键---具有『命令补全』不『档案补齐』的功能

\[Ctrl\]-c按键---让当前的程序『停掉』

\[Ctrl\]-d按键---通常代表着：『键盘输入结束\(End Of File, EOF 戒 End OfInput\)』的意思；另外，他也可以用来取代

exit

5、惯用的关机指令：shutdown

![](http://p1.pstatp.com/large/2890000070014f12f59b "Linux 常用基础命令")

此外，需要注意的是，时间参数请务必加入指令中，否则shutdown会自动跳到 run-level 1 \(就是单人维护的登入情况\)，这样就伤脑筋了！底下提供几个时间参数的例子吧：

![](http://p1.pstatp.com/large/288e0002aed1ddc306ee "Linux 常用基础命令")

# Linux 常用基础命令\(2\)

1、切换执行等级： init

Linux共有七种执行等级：

--run level 0 :关机

--run level 3 :纯文本模式

--run level 5 :含有图形接口模式

--run level 6 :重新启动

使用init这个指令来切换各模式：

如果你想要关机的话，除了上述的shutdown -h now以及poweroff之外，你也可以使用如下的指令来关机：

![](http://p9.pstatp.com/large/28900004149db0f10941 "Linux 常用基础命令\(2\)")

2、改变文件的所属群组：chgrp

![](http://p3.pstatp.com/large/288f0004f166d11b4d4a "Linux 常用基础命令\(2\)")

3、改变文件拥有者：chown

还可以直接修改群组的名称

![](http://p3.pstatp.com/large/288f0004f1beef62de26 "Linux 常用基础命令\(2\)")

4、改变文件的权限：chmod

权限的设定方法有两种， 分别可以使用数字或者是符号来进行权限的变更。

--数字类型改变档案权限：

![](http://p1.pstatp.com/large/2891000380f4ca74a1d8 "Linux 常用基础命令\(2\)")

--符号类型改变档案权限：

![](http://p1.pstatp.com/large/2894000376de4964b803 "Linux 常用基础命令\(2\)")

5、查看版本信息等

![](http://p9.pstatp.com/large/2897000173ff4f955d92 "Linux 常用基础命令\(2\)")

  
Linux 常用基础命令\(3\)

1、变换目录：cd

![](http://p1.pstatp.com/large/289900012b061f3fd95c "Linux 常用基础命令\(3\)")  


2、显示当前所在目录：pwd

![](http://p1.pstatp.com/large/28920002c666305c536f "Linux 常用基础命令\(3\)")

3、建立新目录：mkdir

![](http://p3.pstatp.com/large/28990001317f549bdaff "Linux 常用基础命令\(3\)")

4、删除『空』的目录：rmdir

![](http://p3.pstatp.com/large/289700044530504aaeca "Linux 常用基础命令\(3\)")

5、档案与目录的显示：ls

![](http://p3.pstatp.com/large/28920002ca02a9b399fe "Linux 常用基础命令\(3\)")

6、复制档案或目录：cp

![](http://p9.pstatp.com/large/28980001caf982136dd2 "Linux 常用基础命令\(3\)")

![](http://p3.pstatp.com/large/28980001cbd783079ed6 "Linux 常用基础命令\(3\)")

# Linux 常用基础命令\(4\)

1、移除档案或目录：rm

![](http://p1.pstatp.com/large/2a3900024afbfcadee8b "Linux 常用基础命令\(4\)")

![](http://p3.pstatp.com/large/2a35000241406c1a64db "Linux 常用基础命令\(4\)")

![](http://p3.pstatp.com/large/2a3d0003991589343cdf "Linux 常用基础命令\(4\)")

2、移动档案与目录，或更名：mv

![](http://p3.pstatp.com/large/2a35000241d815c6e2d2 "Linux 常用基础命令\(4\)")

![](http://p3.pstatp.com/large/2a3a000160267734a61b "Linux 常用基础命令\(4\)")

3、取得路径的文件名与目录名：basename，dirname

![](http://p3.pstatp.com/large/2a3e0001cb97c9b1e227 "Linux 常用基础命令\(4\)")

4、由第一行开始显示档案内容：cat

![](http://p3.pstatp.com/large/2a3e0001cc7b63f7d6d2 "Linux 常用基础命令\(4\)")

![](http://p3.pstatp.com/large/2a3c0004280c223c8751 "Linux 常用基础命令\(4\)")

5、从最后一行开始显示：tac（可以看出 tac 是 cat 的倒着写）

![](http://p1.pstatp.com/large/2a3900024d3add56ae19 "Linux 常用基础命令\(4\)")

