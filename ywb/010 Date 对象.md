#### 1 Date 对象   

##### 1.1 创建Date对象    
```JavaScript
var date = new Date();  //获取标准时间
var date1 = new Date("January 12,2006 22:19:35");  //指定时间转换标准时间
var date2 = new Date("month dd,yyyy hh:mm:ss");
var date3 = new Date("month dd,yyyy");
var date4 = new Date(yyyy,mth,dd,hh,mm,ss);
var date5 = new Date(yyyy,mth,dd);
var date6 = new Date(ms);
```

##### 1.2 方法  
|方法|效果|
|:--|:--|
|date.getFullYear()|2017　　从 Date 对象以四位数字返回年份|
|date.getMonth()|11　　    从 Date 对象返回月份 (0 ~ 11)  |
|	 date.getDay()　　      	      |2　　       从 Date 对象返回一周中的某一天 (0 ~ 6)  |
|date.getDate()　　   	  |12　　     从 Date 对象返回一个月中的某一天 (1 ~ 31) |
| date.getHours()　　 	|23　　     返回 Date 对象的小时 (0 ~ 23)|
|date.getMinutes()　  	     |30　　    返回 Date 对象的分钟 (0 ~ 59)  |
| date.getSeconds()　           |54　　    返回 Date 对象的秒数 (0 ~ 59)  |
| date.getMilliseconds()　　|               返回 Date 对象的毫秒(0 ~ 999)  |
| date.getTime()　　		|               返回 1970 年 1 月 1 日至今的毫秒数  |

##### 1.3 字符串化    
* toString():输出：Tue Jul 01 2014 00:00:00 GMT+0800 (中国标准时间)  
* toLocaleString(),输出：2014-06-04  
* toDateString(),输出：Tue Jul 01 2014  
* toLocaleDateString()，输出“2014-06-01”  
* toTimeString(),输出：00:00:00 GMT+0800 (中国标准时间)  
* toLocaleTimeString(),输出：00:00:00  
* valueOf(),与getTime()一样，返回date对象的时间戳  
##### 1.4 获取当前时间  
* Date.now() ,直接返回当前时间对应的时间戳  
##### 1.5 返回时间戳  
* Date.parse(datestr),返回时间戳,参数datestr有两种格式：  
1)YYYY/MM/DD HH:mm:ss (推荐使用)  
2)YYYY-MM-DD HH:mm:ss (在IE中返回NAN)  