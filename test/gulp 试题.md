# gulp 试题
#### [作者] 杨海月
#### [邮箱] yanghaiyue@haomo-studio.com
#### [版本] v1.0.0
#### [标签] 
* gulp 进阶

## [选择题] 1. gulp的API不包括
#### 标签
* gulp

#### [选项]
* A.gulp.src();
* B.gulp.dest();
* C.gulp.end();
* D.gulp.task();

#### [答案]
* C.gulp.end()


## [选择题] 2. gulp.src(globs[, options])API下列说法正确的是
#### 标签
* gulp

#### [选项]
* A.返回的stream不可以被piped到别的插件中;
* B.glob可直接写文件的路径;
* C.options的参数是options.cwd和options.mode;
* D.options.buffer的默认值是false;

#### [答案]
* B.glob可直接写文件的路径

## [选择题] 3. 下列说法错误的是
#### 标签
* gulp 

#### [选项]
* A.js/app.js 精确匹配文件;
* B.!js/app.js 从匹配结果中排除js/app.js;
* C.*.+(js|css) 匹配根目录下所有后缀为.js或者.css的文件;
* D.js/*/.js 匹配js子目录下所有后缀为.js的文件(不包括js文件的.js文件);

#### [答案]
* D.js/*/.js 匹配js子目录下所有后缀为.js的文件(不包括js文件的.js文件)


## [选择题] 4. gulp.dest(path[, options])API下列说法正确的是


#### 标签
* gulp

#### [选项]
* A.options.cwd的cwd参数，只在所给的输出目录是相对路径时有效;
* B.能被 pipe 进来，但不会写文件;
* C. 文件所给的路径是绝对路径;
* D.文件路径和.src()的base的文件路径没关系;

#### [答案]
* A.options.cwd的cwd参数，只在所给的输出目录是相对路径时有效



## [选择题] 5. gulp.task(name[, deps], fn)API说法错误的是

#### 标签
* gulp

#### [选项]
* A.deps任务列表的数组，这些任务会在你当前任务运行之前完成;
* B.任务可以异步执行;
* C.name值可以为空;
* D.task将会以最大并发数执行;

#### [答案]
* C. name值可以为空;


## [选择题] 6. gulp.watch()说法错误的是
#### [标签]
* gulp

#### [选项]
* A、写法gulp.watch(glob [, opts], tasks);
* B、写法gulp.watch(glob [, opts, cb]);
* C、 glob 字符串，或者一个包含多个 glob 字符串的数组，用来指定具体监控哪些文件的变动;
* D、返回改动文件的结果;

#### [答案]
* D、返回改动文件的结果;


## [选择题] 7. 下列说法错误的是
#### 标签
* gulp

#### [选项]
* A.只能执行多个task;
* B.cb(event)，每次变动需要执行的 callback;
* C. callback 会被传入一个名为 event 的对象。这个对象描述了所监控到的变动;
* D.cb是string类型;

#### [答案]
* D.cb是string类型;


## [选择题] 8. event.type的类型不包含
#### 标签
* gulp

#### [选项]
* A.checked
* B.changed
* C.deleted
* D.added

#### [答案]
* A.checked





