# Things must know about webpack

### Why Webpack
- Webpack 有完备的代码分割方案，可以实现动态加载

### 模块化
- CommonJS有缓存机制，同一个模块加载两次只会执行一次
- ES6 Module 默认为严格模式，从其他模块化转过来需要注意
- CommonJs 与ES6 Module 最本质的区别是：前者对模块的依赖是动态的，后者对模块的依赖是静态的；在导出一个模块时，对于前者来说，是值拷贝，对于后者来说是动态映射（引用拷贝）

### 配置
- entry 可以接收多种形式：字符串、数组、对象、函数
- rules 中的exclude 比include 优先级更高
- 被加载的资源模块是resource，加载的资源模块是issuer，这两个都可以在配置里面写
- enforce 可以指定loader 的执行顺序：只能接收pre 或post 两个字符串
- cacheDirectory 可以用于设置babel 编译结果的缓存路径

### About loaders
- loader 其实就是一个函数，要写一个loader，就要定义它的输入和输出
- webpack 只认识js 文件，想要让webpack 像对待js 一样处理其他类型的文件就需要针对指定的文件使用指定的loader 辅助操作
- 常用的loader 包含css-loader、ts-loader、babel-loader、file-loader 等
- babel-loader 相当于是babel-core 和Webpack 的粘合剂；scss-loader 相当于node-sass 和Webpack 的粘合剂
- file-loader 用来处理文件，url-loader 与file-loader 类似，但它可以指定一个阈值，小于这个阈值的图片会处理成base64
- css-loader 和scss-loader 可以通过配置sourceMap 选项查看源码

### About Plugin
- Plugin 是用来扩展webpack 的功能的，通过在构建流程里注入钩子实现各种各样与构建相关的事情
- 常用的Plugin 包含commons-chunk-plugin、uglifyjs-webpack-plugin、happypack-plugin 等
- stylelint 可以用于检查css 风格，但是我们一直都没有用到
- common chunk 的规则是可以定义的，比如说必须被几个以上的文件引用，或者说位于node_modules 下，或者是特定的包（比如react）
- HashModuleIdsPlugin 可以使生成的hash 值更稳定
- Happy pack 可以用于多线程打包

### Sth I didn't know
- npm i --production 就不会安装devDependencies
- webpack-dev-server 将打包结果放在内存中
- 热更新有一个更洋气的名字：live-reloading
- map文件会很大，但是不打开f12，浏览器不会加载这些文件，因此对于普通用户来说并无影响
- 可以通过设置hidden-suorce-map 取消bundle 文件中对map 文件的引用
- 有个叫Import cost 的VS Code 插件可以实时显示引入模块的大小，及gzip 后的大小
- 增加构建速度的两种方法：增加资源（Happy pack）和缩小范围（tree shaking）
- 添加noParse 可以使该模块不被任何loader 解析，但是依然会被打包；IngorePlugin 则不会打包指定模块
- 动态链接库（dll plugin）和code spliting 的区别在于，前者是单独配置，独立打包，理论上来说打包速度更快
- tree shaking 只针对ES6 Module，CommonJs 不好使
- 其他工具：webpack-dashboard、webpack-merge、size-plugin
- HMR 部分刷新页面需要浏览器和WDS（webpack-dev-server）通信
- rollup 可以做到零配置，打包干净，但是只针对js 文件；parcel 打包速度快更快，因为不需要多次转换为AST
