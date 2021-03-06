
### 知识点
- go 语言的吉祥物是gopher，也就是地鼠的英文名，所以写go 的人出去做自我介绍的时候可以这样说：我是一个gopher，因为我写代码的时候像打地鼠一样，bug 一个接着一个
- go 是强类型语言，类型声明写在变量后面
- defer 语句在当前函数执行完毕以后再执行
- 方法和函数的不同之处在于，方法存在接收者，类似于C++ 中类的方法
- 接口，暂时不表
- 拼接字符串使用缓存区效率更高，关于效率的对比可以使用基准测试进行
- 声明数组时，必须指定长度和类型，数组长度不可变，要改变长度需要声明为切片
- 值传递的时候会进行深拷贝，所以如果想要改变传入的变量需要使用地址传值
- reflect 包可以检测变量的类型
- 已声明未初始化的变量默认为零值
- 当标识符（包括常量、变量、类型、函数名、结构字段等等）以一个大写字母开头，如：Group1，那么使用这种形式的标识符的对象就可以被外部包的代码所使用（客户端程序需要先导入这个包），这被称为导出（像面向对象语言中的 public）
- 我们还可以使用 go build 命令来生成二进制文件
```
$ go build hello.go 
$ ls
hello    hello.go
$ ./hello 
Hello, World!
```
- 简短变量声明，`:=`，只能在函数中使用
```
v_name := value
```
- Unicode 是一个标准，而utf8 实现了这个标准
- 跟字符串相关的操作可以使用strings 包 
- 可以使用golint 进行代码风格的检查
- gofmt 格式化、godoc 文档、delve 断点调试、TOML

### Goroutine
- 并发就是同时处理很多事情，并行就是同时做很多事情
- node 和nginx 使用事件循环来实现并发
- 使用通道进行信息的发送和接收

### 书写习惯
- if-else 后的内容不需要带小括号
- go 语言中常量不需要全部大写

### 需要注意
- 目录结构不同，$GOPATH/src/project
- 有大量的错误处理逻辑
- 方法是集中在某一个包里，比如strings
- go 语言将错误作为返回值，这只是他做出的一种设计决策，但对这种处理错误的方式仍存在争议。这种特性使错误处理更加灵活，他让方法或函数的调用者自己决定如何处理错误
- go get 安装包的特性跟deno 有点像，天然去中心化
- 在写go 语言代码之前一定要明确【Go 语言惯常方式】
