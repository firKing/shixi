# 使用typescript编写react
##环境搭建
- 安装 [node.js](https://nodejs.org/en/)
- 安装 typescript `$ npm install -g typescript tsd`    [tsd是什么?](https://www.npmjs.com/package/tsd)
- 推荐一个 [chrome的react开发插件](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)

## 创建一个项目
- 根目录 `$ mkdir typescript`
- 创建一个项目 `$ cd typescript npm init` 这样会创建一个 package.json 文件, 在这个文件中写入项目信息和依赖
```
// package.json 当中加入下面依赖
{
	private: true,
	dependencies: {
  		director: "^1.2.0",
 		react: "^15.0.0",
  		todomvc-app-css: "^2.0.0"
	}
}
```

- 安装依赖 `$ npm install`

##TypeScript类型定义文件
- 类型定义文件通常用于定义公用的第三方库文件API接口, 比如React
- 类型定义文件也用于编译器来确保我们正确地使用第三方库
- 个人认为这种类型定义文件的作用就是如何正确的把ts文件转换成js文件
```
// 在根目录执行 
$ tsd init
$ tsd install react --save
$ tsd install react-dom --save
```
## TypeScript配置文件

- 新建一个文件夹`$ mkdir js`
- 在新建的文件夹下, 创建一个typeScript配置文件`$ tsconfig.json`
- **file属性**:  内部包含要编译的文件或文件夹
- **exclude属性**:  内部包含不被编译的文件或文件夹
- ***两个属性不能同时使用, 同时使用时只有file会生效**
- 在此文件夹下编写ts文件

## 编译TypeScript文件

- 在根目录下执行`$ tsc -p js` 编译指定目录下的ts文件, 在相同目录下会生成对应的js文件