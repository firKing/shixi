# 关于nodePackage

## 起因

我写了一个node包, 是一个模块化的js,  有require引用, 也有module.exports导出;

我知道webpack可以帮忙把文件的依赖关系解决, 从而能够在前端直接引用模块化的js文件, 也可以利用babel解决语法问题利用uglify进行文件压缩;

我用webpack压缩了我的模块化的js代码;

然后再用require引用时, 文件就引用不到了!