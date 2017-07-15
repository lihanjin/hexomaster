---
title: webpack创建vue和vue-router
date: 2017-05-13 22:24:08
tags: Vue
categories: Vue
---
## 一、Vue
1.安装脚手架工具 （只需要安装一次）

	npm install --global vue-cli   /  cnpm install --global vue-cli


2.创建项目

	1.cd到项目所在目录

	2.官方 vue init webpack my-project （不推荐）

	  推荐这样创建项目。

	  vue init webpack-simple my-project  (没有语法检查)

	  vue init webpack-simple固定写法    my-project 项目名称


3.cd 到这个项目里面    `cd my-project` 


4.安装依赖     `npm install  / cnpm install`


5.运行  `npm run dev`

6.编译打包 `npm run build`



1.安装`vue-resource`

	`npm install vue-resource  --save / cnpm install vue-resource  --save`
	`npm install vue-resource  --save-dev`



2.引入`vue-resource`
	`import VueResource from ‘vue-resource’`


3. `Vue.use(VueResource)`;  /*任何插件引入以后都必须use一下

4.其他页面里面使用


----------


## 二、`Vue-router`
1.安装`vue-router      npm install vue-router  --save`

2.引入`vue-router`
	`import VueRouter from 'vue-router'`

	`Vue.use(VueRouter)`


3.创建组件，引入组件

4.配置路由

```
const routes = [
  { path: '/home', component: Home },
  { path: '/news', component: News }
]
```

5.实例化`VueRouter`

	

```
const router = new VueRouter({
	  routes // （缩写）相当于 routes: routes
	})
```

6.挂载到`vue`实例上面

	

```
new Vue({
		  el: '#app',
		  router,
		  render: h => h(App)
	})
```

7. `App.vue`一定注意配置 组件显示的视图

	

```
<router-view></router-view>
```


----------


## 三、`gulp`和`webpack`一样是`web`工程构建工具

`gulp`对项目文件进行流程控制。
要进行模块化，需要借助`require.js`

`webpack：gulp`有的功能，`webpack`都有。
模块化：一个`js`文件就是一个独立的隔绝的作用域。可以把`js`文件当成一个对象。
	在模块化中，如果a文件需要访问b文件的内容，需要向外暴露出去。
	
模块化的方式：
	1).`require.js` ----->> 遵循amd规范
    
	2).`es6 model`
		输出
		`export`
		引入
		`import`
	
	3).node.js提供的 ----->>  common.js规范
		//向外暴露
		module.exports = <需要暴露的内容>;
		//引入其他文件暴露的内容
		//路径的写法：
			1.如果从当前路径找文件需要写'./'
			2.如果从node_modules中找模块，就直接写模块名字
			2.如果从node_modules中找模块，就直接写模块名字，如果找不到，就会从node内置中找，
				还找不到就抛出异常。
		var obj = require('相对路径');
	
`webpack`支持的以上模块化的模块化方式
借助`loader`，插件，预设去处理文件。


使用`webpack `
1.安装
`npm install -g cnpm --registry=https://registry.npm.taobao.org`
	全局安装
	`cnpm install -g webpack`
	查看版本
	`webpack -v`
	本地安装(在项目路径下安装)
	`cnpm init   ---创建package.json文件`
	`cnpm install webpack --save-dev`
		`//卸载：cnpm uninstall webpack --save-dev`
	简写：`cnpm i webpack -D`
	完成后在`package.json`文件中出现：
		//项目的开发依赖，指项目在开发过程中需要用到插件，但是在发布项目后不再需要使用。
		`"devDependencies": {
		    "webpack": "^3.1.0"
		  }`
		//项目的生产依赖，指项目在开发过程中需要用到插件，但是在发布项目后还需要使用。
		例：
		

```
cnpm install jquery --save
			cnpm install jquery -S
			完成后在package.json文件中出现:
			"dependencies": {
			    "jquery": "^3.2.1"
			  }
```

`webpack`操作：
1.`webpack`编辑js文件。
//使用`webpack`编译文件
`webpack` 源文件 目标文件

2.`webpack`配置后编译,`webpack`配置文件:`webpack.config.js`:

```
module.exports = {
	//入口文件
	entry: './js/b.js',
	//输出文件
	output: {
		path: __dirname, //__dirname是nodejs的全局变量,指的是当前路径
		filename: 'js/app.js'
	}
}
```


3. 如果只有`webpack`那么只能编译`JavaScript`文件。
	如果需要编译其他文件，`css，html，es6，vue，jsx，ts。。。。`
     `loader`加载器
     `plugin` 插件   `es6箭头函数`  `es6promise  es6modle  es6class`
     `preset` 预设    `es6`所有插件打包好做成预设
   
   	编译`css`文件需要两个`loader：css-loader style-loader`

	编译`es6`语法的`loader:babel-loader`
	第一次安装还需要安装`babel`命令
	`npm install -g babel-cli`
	安装
	`npm install babel-loader babel-core -D`
		`//babel-loader:babel加载器`
	`	//babel-core:babel核心语法`
`	es6`的预设
	`npm install babel-preset-es2015 -D`
	
	babel编译规则需要.babelrc文件配置
	
	












