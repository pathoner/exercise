# exercise
一些好玩C语言题转换成JS的做法

# 1 使用*来画正方形
在我们学习C语言的时候，开始的几节课老师总是会教我们使用C语言的 printf("***\n")来打印正方形。类似下边的代码: 
``` c
printf("****\n");    
printf("****\n");     
printf("****\n");
```               
然后它就输出:<br>
              ****      
              ****      
              ****<br>
当然了这种方法看起来虽然很友好。但是完全不能体现编程的思想，所以我们需要换另一个方法。接下来我将用JS完成正方形的绘画。
正好自己也能做一些复习。接下来放出代码：
``` javascript
// 先画出正方形的一条边
var square = function(w) {
	var s = ""
		for(var i = 0; i < w; i++) {
			s = s + "#"
		}
	return s =  s + "\n"
}
// square(5)
// 然后将这条边循环几次
var square_n = function(w, h) {
	var a = ""
	for(var i = 0; i < h ; i++) {
		a = a + square(w)
	}
	return a 
}
square_n(5, 5)
```
总结如下：我们在画正方形的时候，可以先试着将正方形的一条边画出来，然后将这条边重复进行循环。最终形成我们所需要的正方形，这也是一种很重要的思想。我称它为
<b>函数化</b>的编程思想。
## 试试： 
1. 试着完成三角形的画法。
2. 试着完成一个方阵。   






# 2 一个乘法表的实现。（可以利用上边的思想进行一个完成）
 自己之前在学习C语言的时候，总是不明白乘法口诀表的实现过程，百度上总是有一堆乱七八糟的教程。好吧，在自己的坚持不懈下，终于能看懂一点点。让我们来看看使用
 C语言的时候要怎么完成乘法口诀表呢。
 ``` c
 # include <stdio.h>
int main()
{
    int i,j;
 for(i=1; i<=9; i++)                       //外层for循环控制列
 {
    for(j=1; j<=i; j++)                    //内层for循环控制行
    {
       printf("%d*%d=%-4d", j, i, i*j);    //%4d表示占4位，不足用空格填充
    }                                      //-4表示左对齐
    printf("\n");
 }
 return 0;
}
```
上述代码，需要使用两个循环，外表的循环控制列，内层的循环控制行的诞生。然而我每次一遇到两个循环互相套的时候，总是会产生许许多多的问题，因而我们要怎么办呢？
接下来就让我们试试怎么引用上边<b>函数化</b>的思想来完成一个乘法口诀表。
``` javascript
// 每一行的诞生，注意此处使用了es6的模板字符串
var addLine = function(number) {
    var s = ''
    for (var i = 0; i < number; i++) {
        var n = i + 1
        // es6模板字符串的使用
         s = s + `${number} * ${n} = ${number*n}  `
       
    }
    return s
}
addLine(2)

var addTable = function() {
    /*
    使用数组将上边addLine 产生的数组存起来
    */
    var table = []
    for (var i = 1; i <= 9; i++) {
        var line = addLine(i)
        table.push(line)
    }
    return table
}
addTable()
```
跟上边的原理一样，我们可以将乘法表进行一个拆分。先画出每一行的，然后在进行一个重复调用，最后诞生！

# 3 接下来我们就要看看什么是递归了
百度上有许许多多的人会告诉你，什么是递归？递归怎么写？有人会告诉你，递归啊！递归就是函数在执行时需要调用自身或者两个函数互相调用。但是，但是这太生涩了。作为一个刚听过这个概念的人，怎么才能明白呢？不过，我准备了一个通俗易懂的东西。
“递归呢就好像查词典，使用的词典，本身就是递归，为了解释一个词，需要使用更多的词。当你查一个词，发现这个词的解释中某个词仍然不懂，于是你开始查这第二个词，可惜，第二个词里仍然有不懂的词，于是查第三个词，这样查下去，直到有一个词的解释是你完全能看懂的，那么递归走到了尽头，然后你开始后退，逐个明白之前查过的每一个词，最终，你明白了最开始那个词的意思。”
接下来，我们看一个例子。
1. 著名经典例子（求阶乘）
阶乘的定义如下<br/>
// n! = n * (n-1)!
放出我们的代码：</br>
``` javascript
var fac = function(n) {
    // 如果 n 是 0 则返回 1
    // 这是递归终止的条件, 没有就会无限递归
    if(n == 0) {
        return 1
    } else {
        // 如果 n 不为 0, 返回 n * fac(n-1)
        // 这时候 n 是已知的, fac(n-1) 需要计算
        // 于是代码进入下一重世界开始计算
        return n * fac(n-1)
    }
}
console.log('递归阶乘', fac(5))
```
递归会有先决条件，当满足某一个条件时，就需要从递归中跳出来。否则就会一直递归，然后爆栈。。（每次在函数调用时，系统会给函数分一块内存来保存变量啊，形参啊，返回值啊，地址等等。）当然了，许许多多的书上总是不会推荐我们使用递归，所以我们平时遇到的递归问题也会很少。作者总是会说，使用递归问题很多很多。像什么内存使用比较多啊，调试不好调试啊。但是，我们也需要正确的去看待问题。有的问题如果比较复杂。使用循环解决起来很费事，想不到解题思路时。在这个时候就可以考虑使用递归啦。<br/>
一般情况下，我们总是会选择使用迭代。也就是循环，一次次去遍历最终解决问题。</br>
比如上边的求阶乘问题，我们就可以倒过来想。可以从1*2*......*n</br>
``` JavaScript
var fac = function(n) {
   // 可以从1开始然后循环乘到 n
    var s = 1
    for (var i = 1; i <=n; i++) {
        s = s * i
    }
    return s
}
console.log("fac",fac(3))
```
## 试试
1. 使用递归完成对斐波那契数的求取。
2. 暂时没想到好作业，下次在说。


## 今天是第几天？
刚开始学习编程的时候，我们总要面对的一个问题就是求闰年，以及今天是多少号？当然了，今天自己试试怎么使用js完成最终效果.<br/>
思考：<br/>
1 怎么才能确定今年是不是闰年？<br/>
2 要确定今天是第几天，需要用月份减1，然后加上日期数<br/>
``` javascript 
<!DOCTYPE html>
<html>
<head>
	<title>今天是第几天</title>
	<meta charset="utf-8">
</head>
<body>
<div class="todo-form">
        <input id='id-input-todo' type="text">
        <button id='id-button-add' type="button">点击</button>
</div>
</body>
</html>
<script type="text/javascript">
	var log = function() {
	    console.log.apply(console, arguments)
	}
	// 用自己实现的 e 替代 document.querySelector
	// 因为这个东西太长了
	var e = function(selector) {
	    return document.querySelector(selector)
	}
	var addButton = e('#id-button-add')
	addButton.addEventListener('click', function(){
		var todoInput = e('#id-input-todo')
    	var todo = todoInput.value
    	var year  = todo.slice(0, 4)  // 获得年份，其实这里应该转成数字
    	var mouth = 1 * (todo.slice(5, 7)) // 同理 这里获得月份 然后假装转成数字
    	// console.log(typeof(mouth))
    	var day = 1 * (todo.slice(8))  // 具体日期
    	var sum = 0 
    	var ping = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31] // 这两个数组比较聪明 存储了每个月的日子
    	var run =  [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
    	// 求闰年/平年函数
    	var isYear = function(year) {
    		if(year % 4 == 0 && year % 100 || year % 400 == 0 ){
    				return 1
    		} else {
    				return 0
    		} 
    	}
    	var days = function(value) {
		if(value == 1 ) {
			for(var i = 0; i < mouth - 1; i++) {
				sum = sum + ping[i] 
			}
				return sum = sum + day
		} else if (value == 0){
			for(var i = 0; i < mouth - 1; i++) {
				sum = sum + run[i] 
			}
			        return sum = sum + day
		}
    	}
    	var value = isYear(year)
    	console.log(days(value))
	} )
</script>
```
实现一个输入框，只不过实在终端查看今天是第几天，后边改成弹窗。


