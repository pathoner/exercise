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









