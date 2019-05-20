### webpack简介
webpack是一个前端模块化打包工具，主要由入口，出口，loader，plugins四个部分。

devDependencies 节点下的模块是我们在开发时需要用的，比如项目中使用的 gulp ，压缩css、js的模块。这些模块在我们的项目部署后是不需要的，所以我们可以使用 -save-dev 的形式安装


### package-lock.json
概括很简单，就是锁定安装时的包的版本号，并且需要上传到git，以保证其他人在npm install时大家的依赖能保证一致。

根据官方文档，这个package-lock.json 是在 `npm install`时候生成一份文件，用以记录当前状态下实际安装的各个npm package的具体来源和版本号。

它有什么用呢？因为npm是一个用于管理package之间依赖关系的管理器，它允许开发者在pacakge.json中间标出自己项目对npm各库包的依赖。你可以选择以如下方式来标明自己所需要库包的版本

这里举个例子：

"dependencies": {
 "@types/node": "^8.0.33",
},

这里面的 向上标号^是定义了向后（新）兼容依赖，指如果 types/node的版本是超过8.0.33，并在大版本号（8）上相同，就允许下载最新版本的 types/node库包，例如实际上可能运行npm install时候下载的具体版本是8.0.35。

大多数情况这种向新兼容依赖下载最新库包的时候都没有问题，可是因为npm是开源世界，各库包的版本语义可能并不相同，有的库包开发者并不遵守严格这一原则：相同大版本号的同一个库包，其接口符合兼容要求。这时候用户就很头疼了：在完全相同的一个nodejs的代码库，在不同时间或者不同npm下载源之下，下到的各依赖库包版本可能有所不同，因此其依赖库包行为特征也不同有时候甚至完全不兼容。

因此npm最新的版本就开始提供自动生成package-lock.json功能，为的是让开发者知道只要你保存了源文件，到一个新的机器上、或者新的下载源，只要按照这个package-lock.json所标示的具体版本下载依赖库包，就能确保所有库包与你上次安装的完全一样。

[package-lock.json | 官方文档](https://docs.npmjs.com/files/package-lock.json)



### semver 语义化版本号变更

`^` 是npm默认的版本符号, 当你使用npm install --save时, npm会自动在package中添加^加上版本号. 例如: npm install --save angular会在package.json中添加"angular": "^1.3.15".这个符号会告诉npm可以安装1.3.15或者一个大于它的版本, 但是要是主版本1下的版本.

`~` 同样被用来做npm得版本控制, 例如~1.3.15, 代表了npm可以安装1.3.15或者更高的版本, 与^的区别在于, ~的版本只能开始于次版本号1.3. 它们的作用域不同. 你可以通过npm config set save-prefix='~'将~设置为默认符号.

`>`符号主要是用来指定可以安装beta版本.

[semver版本号 | 官方文档](https://semver.org/lang/zh-CN/)