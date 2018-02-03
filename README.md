# php_Date-and-time
php_的日期与时间

    	1. 介绍UNIX时间戳
   		以32位整数表示格林威治标准时间  11230499325
 
 		  这个UINIX时间戳整数是从1970年1月1日0时0分0秒（计算机元年）到现在的秒数
 		  作用：方便我们计算使用（参于运算）
 
 
  		1970---2038  
 
 
  	2. 在PHP中获取日期和时间 
 
  		time()    返回当前的 Unix 时间戳
  		getDate()  取得日期／时间信息
  		gettimeofday() 取得当前时间
  		date_sunrise() 返回给定的日期与地点的日出时间
  		date_sunset()   返回给定的日期与地点的日落时间
 
 
  	3. 日期和时间的格式化输出
  		  将时间戳的格式转了 我们可以读懂的时间格式
  	  	date(string, [timestamp]);
 
  	4. 将日期和时间转变成UNIX时间戳
  		  mktime()
        mktime(时,分,秒,月,日,年)


     cho time()."<br>";    输出：1517636059
     echo mktime()."<br>"; 输出：1517636059
     echo date("Y-m-d H:i:s", mktime(12, 30, 44))."<br>"; 输出 2018-02-03 12:30:44
     echo date("Y-m-d H:i:s", mktime(0, 0, 0, 8,12,2002))."<br>";输出 2002-08-12 00:00:00

    5. 修改PHP的默认时区
    		php.ini
    		date.timezone=
   
       date_default_timezone_set("PRC");
           Asia/Shanghai
           PRC
           Gtc/GET-8 
       
       
    例子 
       算出年龄

          $birthday="1992-7-20"; // 客人生日
          $date=date("Y-m-d");    //取当前时间
          list($y,$m,$d)=explode("-",$birthday); //  按“-”分割生日的日期
          list($xy,$xm,$xd)=explode("-", $date);   //按“-”分割当前的日期
      
           $age=$xy-$y;  //当前年份减去客人出生年份
           echo $age;  输出 26



















