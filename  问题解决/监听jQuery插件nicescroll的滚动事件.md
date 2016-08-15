# 监听jQuery插件nicescroll的滚动事件

## 问题描述

​	在项目项目中用了jQuery的nicescroll插件, 想监听插件的滚动条到底部时做出一些处理, 一开始直接试了`$(window).scroll()`方法, 但是鼠标滚轮事件被插件管理了(配置项`enablemousewheel`，nicescroll可以管理的鼠标滚轮事件（默认：true）), 所以并不能监听到, 网上搜了一下也没找到好的解决办法

## 问题解决

​	既然滚轮事件被插件对象管理了, 那么也一定做了处理, 所以我开始在创建的插件对象上面做文章. 我在对象里面找到了这个方法:

![CDD03226-62EE-4B15-B452-BC8DBC6B4CEA](/Users/baidu/Library/Containers/com.tencent.qq/Data/Library/Application Support/QQ/Users/854650893/QQ/Temp.db/CDD03226-62EE-4B15-B452-BC8DBC6B4CEA.png)

然后心里想: "嗯, 调用这个函数应该可以了吧", 可是没想到: 

![9FC7411A-251B-4344-B7A8-899D534F3001](/Users/baidu/Library/Containers/com.tencent.qq/Data/Library/Application Support/QQ/Users/854650893/QQ/Temp.db/9FC7411A-251B-4344-B7A8-899D534F3001.png)

这特么就尴尬了, 于是继续找, 看到了这个:

 ![58279A14-D310-4DD8-917B-9FBA0187907C](/Users/baidu/Library/Containers/com.tencent.qq/Data/Library/Application Support/QQ/Users/854650893/QQ/Temp.db/58279A14-D310-4DD8-917B-9FBA0187907C.png)

然后试了一下:

![4DD8B28C-D3A8-464E-A1F5-8F34C4CF5A88](/Users/baidu/Library/Containers/com.tencent.qq/Data/Library/Application Support/QQ/Users/854650893/QQ/Temp.db/4DD8B28C-D3A8-464E-A1F5-8F34C4CF5A88.png)

​	哦豁, 这个可以, 就它了, 但是新问题出现了, 现在可以监听滚动事件了, 但是怎么判断滑动到底部了呢? 我在页面上发现了几个参数 :![63e003c1638127bcc85d70024e8921c3](/Users/baidu/Library/Caches/BaiduMacHi/Share/images/63e003c1638127bcc85d70024e8921c3.png)

​	外面这个div是滚动条, 里面包含的div是滚动条的游标(cursors), 看这三个参数: 第一个是滚动条的高度, 第二个是游标的相对移动位置, 第三个是游标的高. 滑到底部时, 第一个正好等于第二个加第三个.

​	于是我想$()获取dom对象获取参数的值然后进行对比, 然后被导师骂 太low了= =, 导师给了个提示, 这个dom是插件对象创建的, 那能不能再插件对象上面获取这些参数呢?

​	是个好主意, 于是又开始在茫茫多的属性和参数当中寻找, 直到我发现了这个: 

 ![9a955a42d6022eac730c942290e7c8ce](/Users/baidu/Library/Caches/BaiduMacHi/Share/images/9a955a42d6022eac730c942290e7c8ce.png)

 ![fa348ff5354aaa50d8ec77bbec7605df](/Users/baidu/Library/Caches/BaiduMacHi/Share/images/fa348ff5354aaa50d8ec77bbec7605df.png)

`newscrolly`是插件对象的一个参数, 值是插件当前的y轴的高度, page.maxh是插件的最大高, 是固定不变的, 所以在之前的scrollend函数当中监听这两个值相等的时候就是滑到底部的时候啦, 就像这样:

```
window.niceSCROLL.scrollend(function(){
            if(window.niceSCROLL.page.maxh == window.niceSCROLL.newscrolly) {
                console.log(1);
            }
        });
```



如果有更好的建议, 欢迎讨论: firkin@126.com