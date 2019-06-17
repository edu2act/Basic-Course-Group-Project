### 5 字符串函数  
javascript字符串函数完成对字符串的字体大小、颜色、长度和查找等文明作，共包括以下20个函数：  
1. anchor函数：产生一个链接点(anchor)以作超级链接用。anchor函数设定<A NAME...>的链接点的名称，另一个函数link设定<A HREF=...>的URL地址。  
2. big函数：将字体加到一号，与<BIG>...</BIG>标签结果相同。  
3. blink函数：使字符串闪烁，与<BLINK>...</BLINK>标签结果相同。  
4. bold函数：使字体加粗，与<B>...</B>标签结果相同。  
5. charAt函数：返回字符串中指定的某个字符。  
6. fixed函数：将字体设定为固定宽度字体，与<TT>...</TT>标签结果相同。  
7. fontcolor函数：设定字体颜色，与<FONT COLOR=color>标签结果相同。  
8. fontsize函数：设定字体大小，与<FONT SIZE=n>标签结果相同。  
9. indexOf函数：返回字符串中第一个查找到的下标index，从左边开始查找。  
```JavaScript
var mystr="Hello world!";
var index=mystr.indexOf("llo");    	//2
var index1=mystr.indexOf("l");    	//2
var index2=mystr.indexOf("l",3);    //3
```
10. italics函数：使字体成为斜体字，与<I>...</I>标签结果相同。  
11. lastIndexOf函数：返回字符串中第一个查找到的下标index，从右边开始查找。 
```JavaScript
var mystr="Hello world!";
var index=mystr.lastIndexOf("llo");    	//2
var index1=mystr.lastIndexOf("l");    	//9
var index2=mystr.lastIndexOf("l",4);    //3
```
12. length函数：返回字符串的长度。(不用带括号)  
```JavaScript
var mystr="qingchenghuwoguoxiansheng,woaishenghuo,woaiziji";
var arrLength=mystr.length;    //47
```
13. link函数：产生一个超级链接，相当于设定<A HREF=...>的URL地址。  
14. small函数：将字体减小一号，与<SMALL>...</SMALL>标签结果相同。  
15. strike函数：在文本的中间加一条横线，与<STRIKE>...</STRIKE>标签结果相同。  
16. sub函数：显示字符串为下标字(subscript)。  
17. substring函数：返回字符串中指定的几个字符。  
```JavaScript
var mystr="hello world!";
var sliceStr1=mystr.substring(3);    	//lo world!
var sliceStr2=mystr.substring(3,7);    	//lo w
```
18. sup函数：显示字符串为上标字(superscript)。  
19. toLowerCase函数：将字符串转换为小写。  
20. toUpperCase函数：将字符串转换为大写。  
```JavaScript
var mystr="Hello World!";
var lowCaseStr=mystr.toLowerCase();    //hello world!
var upCaseStr=mystr. toUpperCase();    //HELLO WORLD!
```






