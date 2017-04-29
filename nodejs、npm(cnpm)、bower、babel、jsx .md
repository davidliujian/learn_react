## nodejs
> Node.js是一个Javascript运行环境(runtime)。实际上它是对Google V8引擎进行了封装。V8引 擎执行Javascript的速度非常快，性能非常好。Node.js对一些特殊用例进行了优化，提供了替代的API，使得V8在非浏览器环境下运行得更好。Node.js是一个基于Chrome JavaScript运行时建立的平台， 用于方便地搭建响应速度快、易于扩展的网络应用。Node.js 使用事件驱动， 非阻塞I/O 模型而得以轻量和高效，非常适合在分布式设备上运行数据密集型的实时应用。

## npm（cnpm:淘宝 NPM 镜像）
> PM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：
> + 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
> + 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
> + 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。
>> 升级npm ：npm install npm -g   
>> 安装模块 ：npm install <Module Name> 

> npm 的包安装分为本地安装（local）、全局安装（global）两种，从敲的命令行来看，差别只是有没有-g而已
>> npm install express          # 本地安装  
npm install express -g   # 全局安装

> 更新模块 npm update express   
搜索模块 npm search express

## bower
> Bower是Web开发中的一个前端文件包管理器。类似于Node模块的npm包管理器，它允许开发者为服务器编写可共享的模块。Bower为Web组件提供了类似的功能。  

> 安装：npm install -g bower    （bower依赖于Git、Node和npm。）     
下载模块： bower install jquery

## babel
> Babel 用于转化你的 JavaScript 代码
- ES2015 以及更多
- JSX 和 React
- 可组合拼装

## jsx
<http://limoer.cc/2016/10/11/React%E5%AD%A6%E4%B9%A0%E4%B9%8BJSX/>  
<http://reactjs.cn/react/docs/jsx-in-depth-zh-CN.html>
> JSX是对javascript的扩展，语法类似于XML，但JSX不是一门新的语言，
确切来说只是语法糖，每一个XML都会被响应的转换工具转换成纯的javascript代码。     


