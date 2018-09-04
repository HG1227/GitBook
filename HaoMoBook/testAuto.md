## 论基础 {#1-测试理论基础}

### 1.1 概念 {#11-概念}

测试分层：

![](https://hxgqh.gitbooks.io/testautomization/content/files/TestPyramid.png "TestPyramid")

#### 1.1.1 TDD {#111-tdd}

Test Drive Development，测试驱动开发

* 对应于单元测试
* 函数、类级别测试

#### 1.1.2 BDD {#112-bdd}

Behavior Drive Development，行为驱动开发

* 对应于用户实际使用情况
* 并不强调对系统功能、性能以及边界值等的健全性做保证

它通过用自然语言书写非程序员可读的测试用例扩展了测试驱动开发方法。行为驱动开发人员使用混合了领域中统一的语言的母语语言来描述他们的代码的目的。这让开发者得以把精力集中在代码应该怎么写，而不是技术细节上，而且也最大程度的减少了将代码编写者的技术语言与商业客户、用户、利益相关者、项目管理者等的领域语言之间来回翻译的代价。

#### 1.1.3 DDD {#113-ddd}

Domain Drive Development，领域驱动开发

### 1.2 测试分类 {#12-测试分类}

从测试设计方法分

```
黑盒测试
白盒测试
灰盒测试
```

从测试目的分

功能性测试

```
*单元测试
功能测试
*集成测试
场景测试
*系统测试
Alpha测试：软件测试人员在真实用户环境中对软件进行全面的测试
Beta测试：真实的用户在真实的用户环境中进行的测试, 也叫公测
*验收测试
```

非功能性测试

```
压力测试
负载测试
性能测试
兼容性测试
安全性测试
代码覆盖率测试
```

参考资料：  
[http://www.jianshu.com/p/6b3d75f5f031](http://www.jianshu.com/p/6b3d75f5f031)  
[http://blog.csdn.net/kerryzhu/article/details/5631960](http://blog.csdn.net/kerryzhu/article/details/5631960)

## 2 测试框架及工具 {#2-测试框架及工具}

代码质量管理平台：

```
Sonar
```

### 前端 {#前端}

![](https://hxgqh.gitbooks.io/testautomization/content/files/前端测试工具.svg "前端测试工具")

#### 参考 {#参考}

[http://efe.baidu.com/blog/front-end-continuous-integration-tools/](http://efe.baidu.com/blog/front-end-continuous-integration-tools/)[http://taobaofed.org/blog/2016/01/08/karma-origin/](http://taobaofed.org/blog/2016/01/08/karma-origin/)

### Java {#java}

![](https://hxgqh.gitbooks.io/testautomization/content/files/Java测试工具.svg "Java测试工具")

## 参考资料 {#参考资料}

[http://www.infoq.com/cn/tdd](http://www.infoq.com/cn/tdd)[http://tech.colla.me/zh/show/understanding\_unit\_test\_and\_e2e\_test\_in\_frond\_end\_development](http://tech.colla.me/zh/show/understanding_unit_test_and_e2e_test_in_frond_end_development)

