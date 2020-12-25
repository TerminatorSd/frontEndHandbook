## Angular 相关



### 细碎的知识点
- encapsulation

### 配置文件必知必会
#### angular.json

#### tsconfig.json

### entryComponent
- entryComponents declarations are deprecated as they are no longer needed

### 差分构建
- 构建结果中包含ES5 和ES6+ 的代码
- ng8 中需要做两次完整构建；ng9 中先构建出ES6，然后转换为ES5

### 如何理解ng9 中的Ivy 和ngcc
- https://indepth.dev/posts/1112/a-look-at-major-features-in-the-angular-ivy-version-9-release
- Ivy 与View Engine
    - Angular libraries cannot be AOT-compiled using View Engine
    - AOT 相比于JIT 能更早发现问题，比如说如果你的html 中引用的ts 变量或者方法在ts 文件中没有定义，AOT 在本地编译就可以发现，而JIT + AOT 则要延迟问题的发现

### Angular 中为什么要有NgModule？
- 问题：Component 已经可以是一个完整的个体
- 每个Component 必须从属于一个Module; 一个Component 不能被两个Module 声明
- import 的最小单位可以是Component 或者Module，在Component 使用类似ngIf 等功能，必须要保证它所在的模块引入了对应的CommonModule 等相关模块
- 一个Module 可以声明多个组件，类似Java 中的package，或者namespace
- 你可以不把组件声明在imports 里面从而产生私有组件
- 编译出哪些标记，以及哪些依赖应该被注入其中
  - Module 可以解决组件重名的问题，没有Module 可能需要在全局注册组件与标签对应关系
  - 为一个Module 注入的依赖可以在多个组件使用

### Redux
- 包含：reducer（实施增减操作的纯函数）、state（状态保存）、action（增减操作）
  - reducer，接收state 和action，返回新的state


