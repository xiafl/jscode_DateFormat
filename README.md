# jscode_DateFormat
将日期转换为指定的格式，从某个字符串中按照指定的格式提取日期。纯js代码，无其它框架或特殊环境依赖


## 背景
当需要将日期转换为指定的格式时，或者需要从某个字符串中按照指定的格式提取日期，均可使用本模块。

## 使用说明  
格式标记的含意:   
yyyy-四位阿拉伯数字的年份，如： 2018  
YYYY-四位中文数字的年份，如： 二零一八  
yy-两位阿拉伯数字的年份，如： 18  
YY-两位中文数字的年份，如： 一八  
mm-一位或两位阿拉伯数字的月数，如： 3 、 12   
0m-两位阿拉伯数字的月数，如： 03 、 12  
MM-一位或两位中文数字的月数，如：  三、 十二   
dd-一位或两位阿拉伯数字的日数，如： 3 、 12   
0d-两位阿拉伯数字的日数，如： 03 、 12、28   
DD-中文数字的日数，如：  三、 十二、二十八   
hh-一位或两位阿拉伯数字的小时数，如： 3 、 12   
0h-两位阿拉伯数字的小时数，如： 03 、 12   
HH-中文数字的小时数，如：  三、 十二、二十三   
ff-一位或两位阿拉伯数字的分钟数，如： 3 、 12、56  
0f-两位阿拉伯数字的分钟数，如： 03 、 12  
0F-中文数字的分钟，如：  零三、 十二、二十三  
FF-中文数字的分钟，如：  三、 十二、二十三   
ss-一位或两位阿拉伯数字的秒数，如： 3 、 12   
0s-两位阿拉伯数字的秒数，如： 03 、 12   
0S-中文数字的秒数，如：  零三、 十二、二十三   
SS-中文数字的秒数，如：  三、 十二、二十三   
w-阿拉伯数字的星期数，如：  1、6、7  
W-中文数字的星期数，如：  一、三、六、日   
WT-中文数字的星期数，如：  一、三、六、天   
  
### 属性  
这些属性是可读可写的，如果直接更改，则会自动计算其关联的其它值。  
dataformat.year; //年 [1000, 3000]  
dataformat.moth; //月 [1, 12]  
dataformat.day; //日 [1, 31]  
dataformat.hour; //时 [0, 23]  
dataformat.minute; //分 [0, 59]  
dataformat.second; //秒 [0, 59]  
dataformat.mscond; //毫秒 [0, 999]  
dataformat.week; //星期 [1, 7]  
dataformat.timestamp; //时间戳  

### 构造函数
构造函数内部直接调用的 setTime(ms, formatStr);
  
### toString(formatStr)  
将日期转换为指定格式，formatStr是格式字符串。  
  
使用举例:   
1. toString() //结果: '2014-11-7 03:08:01'  
2. toString('yyyy-mm-dd hh:ff:ss') //结果: '2014-11-11 13:12:34'  
3. toString('yyyy年mm月dd日') //结果: '2014年11月11日'  
4. toString('yy年mm月dd日') //结果: '14年11月11日'  
5. toString('YY年MM月DD日') //结果: '一四年十一月八日'  
6. toString('星期W') //结果: '星期日'  或 '星期三'
7. toString('星期WT')  //结果: '星期天'  或 '星期三'
8. toString('星期w') //结果: '星期1'   或 '星期7'
9. toString('hh:0f:ss') //结果: '3:04:5'  
10. toString('date') //结果: '2014-11-7'  
11. toString('time') //结果: '03:08:01'  
  
### setTime(ms, formtStr)  
设置时间。如果存在 formatStr， 则表示从字符串 ms 中按 formatStr中的规则提取时间。  
  
使用举例:  
1. setTime( new Date() ); //传入一个时间对象  
2. setTime( new Date().getTime() ); //传入一个毫秒数  
3. setTime( new Date().getTime() ); //传入一个毫秒数  
4. setTime( new Date().getTime() + '' ); //传入一个毫秒数的字符串  
5. setTime(); //传入其它的值或不传入，则创建当前时间  
6. setTime(str, formatStr); //传入两个参数，第一个为字符串，第二个为格式规则，表示按照规则从字符串中提取时间  
7. setTime('今天是2014年8月9号，天气特别好，但明天是2014年8月10号，....', '明天是yyyy年mm月dd号');  // 得到  2014.8.10 0:0:0
  
### fillChar(num, len, char)  
字符填充  
  
使用举例:   
1. fillChar(44, 5, '*'); //结果: '***44'   
2. fillChar(44, 5); //结果: '00044'   
3. fillChar('44', 5); //结果: '   44'   
4. fillChar('aaa', 5); //结果: '   aa'   
5. fillChar('aaa', 5, '$'); //结果: '$$aaa'   
5. fillChar('aaa', 1, '$'); //结果: 'aaa'  //指定的长度太小，不做任何操作。  
  
### perNumToChinese(num)  
将阿拉伯数字每一位对应转换为中文的格式。  
  
使用举例:   
1. perNumToChinese(34); //结果: '三四'  
2. perNumToChinese(3874); //结果: '三八七四'  
3. perNumToChinese('3874'); //结果: '三八七四'  
4. perNumToChinese('404'); //结果: '四零四'    
5. perNumToChinese('0  04   '); //结果: '零零四'  
6. perNumToChinese('  '); //结果: ''  
  
### perChineseToNum(numStr)
将中文的格式的数字每一位对应转换为阿拉伯数字。 是perNumToChinese(num)的逆操作。  
  
使用举例:   
1. perChineseToNum('三四'); //结果: 34  
2. perChineseToNum('三八七四'); //结果: 3874  
3. perChineseToNum('四零四'); //结果: 404  
4. perChineseToNum('零零四'); //结果: 4  
5. perChineseToNum('  '); //结果: NaN  
  
### numToChinese(num)  
将阿拉伯数字转换为中文的格式 , 最多只能处理13位数(万亿)  
  
使用举例:   
1. numToChinese(0); //结果: '零'  
2. numToChinese(5); //结果: '五'  
3. numToChinese(16); //结果: '十六'  
4. numToChinese(34); //结果: '三十四'  
5. numToChinese(106); //结果: '一百零六'  
6. numToChinese(886); //结果: '八百八十六'  
7. numToChinese(1004); //结果: '一千零四'  
8. numToChinese(1000); //结果: '一千'  
9. numToChinese(9904); //结果: '九千九百零四'  
10. numToChinese(19904); //结果: '一万九千九百零四'  
11. numToChinese(10004); //结果: '一万零四'  
12. numToChinese(10000); //结果: '一万'  
13. numToChinese(100404); //结果: '十万零四百零四'  
14. numToChinese(9000000); //结果: '九百万'  
15. numToChinese(90000000); //结果: '九千万'  
16. numToChinese(900000000); //结果: '九亿'  
17. numToChinese(9000000000); //结果: '九十亿'  
18. numToChinese(9020030401); //结果: '九十亿零二千零三万零四百零一'  
19. numToChinese(90000000000); //结果: '九百亿'  
20. numToChinese(900000000000); //结果: '九千亿'  
21. numToChinese(9000000000000); //结果: '九万亿'  
22. numToChinese(90000000000000); //结果: undefined  
  
  
### chineseToNum (numStr)
将中文的格式的数字转换为阿拉伯数字, 最多只能处理13位数(万亿)。 是 numToChinese(num) 函数的逆操作。  
  
使用举例:   
1. chineseToNum('十六'); //结果: 16  
2. chineseToNum('一万九千九百零四'); //结果: 19904  
3. chineseToNum('十万零四百零四'); //结果: 100404   
4. chineseToNum('九十亿零二千零三万零四百零一'); //结果: 9020030401  
  
  
## 注意事项  

