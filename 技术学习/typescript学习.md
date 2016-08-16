# typescript学习

## 开始

### 安装

​	执行 	`npm install -g typescript tsd`	[tsd是什么?](https://www.npmjs.com/package/tsd)

​	tsd是用来安装类型定义文件的, 类型定义文件通常用于定义公用的第三方库文件API接口, 比如React, 类型定义文件也用于编译器来确保我们正确地使用第三方库, 个人认为这种类型定义文件的作用就是如何正确的把ts文件转换成js文件

### tsconfig.json

​	如果一个目录下存在一个`tsconfig.json`文件，那么它意味着这个目录是TypeScript项目的根目录。`tsconfig.json`文件中指定了用来编译这个项目的根文件和编译选项。

`files`属性和`exclude`属性

### 三斜线指令

​	三斜线指令是包含单个XML标签的单行注释。 注释的内容会做为编译器指令使用。`///  <reference path="..." />`指令是三斜线指令中最常见的一种。 它用于声明文件间的 *依赖*。

## 命名空间

- 使用命名空间是为了提供逻辑分组和避免命名冲突。
- 任何使用`module`关键字来声明一个"内部模块"的地方都应该使用`namespace`关键字来替换。
- 如果允许在命名空间之外访问记得加`export`
- 在命名空间外访问的时候需要限定类型的名称

## 基础类型

- 布尔: boolean


- 数字: number


- 字符串: string

- 数组: Array<number>; number[]

- 元组: [string, number]

- 枚举: enum

- 任意类型: any

- 空值: void

- null 和 undefined

- 类型断言(类型转换):

  类型断言有两种形式。 其一是“尖括号”语法：

  ```
  let someValue: any = "this is a string";

  let strLength: number = (<string>someValue).length;

  ```

  另一个为`as`语法：

  ```
  let someValue: any = "this is a string";

  let strLength: number = (someValue as string).length;
  ```

## 变量声明

- var: 函数级作用域


- let: 块级作用域

  - 不能在块之外访问

  - 不能在被声明之前读或写

  - 不能在同一个作用域多次声明同一个变量

  - let在循环体里时, 每次迭代都会创建一个新作用域

  - ```
    for (let i = 0; i < 10 ; i++) {
        setTimeout(function() {console.log(i); }, 100 * i);
    }
    ```


- const: 静态常量

- 解构数组

  作用于函数参数：

  ```
  function f([first, second]: [number, number]) {
      console.log(first);
      console.log(second);
  }
  f(input);

  ```

  也可以使用`...name`语法创建一个剩余变量列表：

  ```
  let [first, ...rest] = [1, 2, 3, 4];
  console.log(first); // outputs 1
  console.log(rest); // outputs [ 2, 3, 4 ]
  ```


- 解构对象

  你也可以解构对象：

  ```
  let o = {
      a: "foo",
      b: 12,
      c: "bar"
  }
  let {a, b} = o;
  ```

## 接口

```
interface LabelledValue {
  label: string;
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```

- 可选属性

  ```
  interface SquareConfig {
    color?: string;
    width?: number;
  }
  ```


- 只读属性

  ```
  interface Point {
      readonly x: number;
      readonly y: number;
  }
  ```


- 函数类型

  ```
  interface SearchFunc {
    (source: string, subString: string): boolean;
  }
  ```


- 可索引的类型

  ```
  interface StringArray {
    [index: number]: string;
  }
  ```


- **类类型***


- 扩展接口

  ```
  interface Shape {
      color: string;
  }

  interface PenStroke {
      penWidth: number;
  }

  interface Square extends Shape, PenStroke {
      sideLength: number;
  }

  let square = <Square>{};
  square.color = "blue";
  square.sideLength = 10;
  square.penWidth = 5.0;
  ```


## 附录

[TypeScript Handbook（中文版）](https://zhongsp.gitbooks.io/typescript-handbook/content/)

