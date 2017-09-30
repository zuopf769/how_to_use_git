## github如何精准分享关键代码

> [左鹏飞](https://github.com/zuopf769) 2017.09.31

### #L行号

比如你有一个文件里的某一行代码写得非常酷炫或者关键，想分享一下。可以在url后面加上 `#L行号`。

比如，点击下面这个url：

[https://github.com/AlloyTeam/AlloyTouch/blob/master/alloy_touch.js#L240](https://github.com/AlloyTeam/AlloyTouch/blob/master/alloy_touch.js#L240)

你便会跳到alloy_touch.js的第240行。


### #L开始行号-L结束行号

那么问题来了？如果我是一段代码，即多行代码想分享呢？也很简单：url后面加上`#L开始行号-L结束行号`.


比如，AlloyTouch的运动缓动和逆向缓动函数如下面代码段所示：
https://github.com/AlloyTeam/AlloyTouch/blob/master/alloy_touch.js#L39-L45

其实也不用自己在网址后面操作，github自动会帮你生成url。

+ 比如你点击39行，url变成了
https://github.com/AlloyTeam/AlloyTouch/blob/master/alloy_touch.js#L39


+ 再按住shift点击45行，url变成了
https://github.com/AlloyTeam/AlloyTouch/blob/master/alloy_touch.js#L39-L45


然后你这个url就可以复制分享出去了，点击这个url的人自动会跳到39行，并且39-45行高亮。

