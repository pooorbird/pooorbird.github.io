## Welcome to Bird's Blog

您可以访问我的[鸟窝](https://pooorbird.github.io/)获取我的动态

### 2017年7月24日 Mysql分组按时间排序

假设有一张表,id是人员id,name是名称,time是访问时间:
<table>
	<tr>
		<th>id</th>
		<th>name</th>
		<th>time</th>
	</tr>
	<tr>
		<td>1</td>
		<td>John</td>
		<td>2017-7-24 10:00:00</td>
	</tr>
	<tr>
		<td>2</td>
		<td>John</td>
		<td>2017-7-24 11:00:00</td>
	</tr>
	<tr>
		<td>3</td>
		<td>Alice</td>
		<td>2017-7-24 12:00:00</td>
	</tr>
	<tr>
		<td>4</td>
		<td>Bob</td>
		<td>2017-7-24 12:00:00</td>
	</tr>
</table>
- 查询所有人最近的访问时间

首先我是这样做的
```SQL
SELECT MAX(u.time) FROM user u GROUP BY u.name
```
取最大值然后分组就可以了,结果却不是这样。

改进后
```SQL
SELECT u.time FROM user u ORDER BY u.time DESC GROUP BY u.name
```
先排序再按人分组，结果和上面一样。本来就是一样的嘛.

百度后。。。group by 优先执行,也就是说不管怎么排序分组后就没有顺序了。
最后使用的方案是子查询
```SQL
SELECT uu.time FROM (SELECT u.time FROM user u ORDER BY u.time DESC LIMIT 1) uu GROUP BY uu.name
```

***

### 2017年7月22日 Markdown语法学习

Markdown 是一种轻量化的模板语言。下面是一些实例，作为下次发博的参考。

```markdown
这是一个大黑框orz 大黑框里面的东西都不会被模板转换。
```
# 这可能是一级标题
## 这是一级标题下面的标题
### 这不是一级标题下面的标题
#### (⊙v⊙)嗯

这是没有顺序的列表
- 滴，学生卡
- 滴。

这是有顺序的列表
1. 起床
2. 睡觉

**我变粗了**

_斜眼笑_

`chengxuyuankanzhezuishufudewenzigeshi`

贴上我的照片
![帅](http://qq.yh31.com/tp/zjbq/201506211824137045.jpg)

子曾经曰过

> 知识就是力量

下面是一段js
```javascript
function sayHelloTosb(name) {
 	alert("hello" + name);
}
```

这个太Low看起来没用

    function fancyAlert(arg) {
      if(arg) {
        $.facebox({div:'#foo'})
      }
    }
    

任务清单
- [x] 吃
- [x] 睡
- [x] 吃
- [ ] 睡

您的支持是我更新的动力吗？不是 :+1:

被占用符号的转义

\*天上的星星\*

\*参北斗啊\*

```java
public class SayHello {
	public void main(String[] args) {
		System.out.println("END");
	}
}
```

```c
#include <stdio.h>
main {
	print("END");
}
```

```sqlserver
select sysdate() FROM dual;
```