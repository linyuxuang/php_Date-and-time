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


   日期
     
       calendar.class.php文件
       
       
     <?php

      class Calendar{
            private $year; //当前的年
            private $month; //当前的月
            private $start_weekday; //当月的第一天对应的是周几
            private $days; //当前月一共多少天
		
       function  __construct(){
           $this->year=isset($_GET["year"]) ? $_GET["year"] : date("Y");
           $this->month=isset($_GET["month"]) ?  $_GET["month"] : date("m");


	  		$this->start_weekday=date("w", mktime(0, 0, 0, $this->month, 1, $this->year));
	  		$this->days=date("t", mktime(0, 0, 0, $this->month, 1, $this->year));
        }		
		
	 function  out(){
		echo "<table  align='center'>";
			$this->chageDate();
			$this->weekeList();
			$this->daysList();
	    echo "</table>";		
		
	 }
	
    private function weekeList(){
	  $wee=array("日","一","二","三","四","五","六");
	  
	  echo "<tr  style='background:green'>";
	  	for($i=0;$i<count($wee);$i++){
	  		echo '<th>'.$wee[$i].'</th>';
	  	}
	  echo "</tr>";	
     }	

    private function daysList(){
			echo '<tr>';
			//输出空格(当前一月第一天前面要空出来)
			for($j=0; $j<$this->start_weekday; $j++)
				echo '<td>&nbsp;</td>';
				  
			for($k=1; $k<=$this->days; $k++){
     			   $j++;
				if($k==date('d'))
					echo '<td class="fontb">'.$k.'</td>';
				else
					echo '<td>'.$k.'</td>';

				if($j%7==0)
					echo '</tr><tr>';
				
			}
			echo '</tr>';
		}

        private function  prevYear($year,$month){
               $year=$year-1;
               if($year<1970){
                  $year=1970;
               }
               return "year={$year}&$month={$month}";
        }

         private function prevMonth($year,$month){
                if($month==1){

                    $year=$year-1;
                 if($year<1970)	
                    $year=1970;

                 $month=12;   
         }else{
            $month--;
         }
            return "year={$year}&month={$month}";
        }

        private function nextYear($year, $month){
                $year=$year+1;
                if($year>2038)
                $year=2038;
                return "year={$year}&month={$month}";
        }

        private function nextMonth($year, $month){
        if($month==12){
             $year++;
         $month=1;
        }else{
            $month++;
        }
           return "year={$year}&month={$month}";
        }
      private function chageDate(){
         echo '<tr>';
             echo '<td><a href="?' .$this->prevYear($this->year,$this->month).' "><<</a></td>';
             echo '<td><a href="?'.$this->prevMonth($this->year, $this->month).'">'.'<'.'</a></td>';
             echo '<td>'.$this->year.' 年'.$this->month.' 月'.'</td>';
             echo '<td><a href="?' .$this->nextMonth($this->year,$this->month).'">></a></td>';
             echo '<td><a href="?' .$this->nextYear($this->year,$this->month).'">>></a></td>';
            echo '</tr>';
          } 
          }
        ?>

  text.php文件


          <style>
            table {
            border:1px solid #050;
           }
        .fontb{
            background: red;
         }
         th{
            width: 30px;
        }
        td,th {
            height:30px;
            text-align:center;

         }
     </style>


    <?php
        @header("content-Type: text/html; charset=utf-8"); //语言强制
          include "calendar.class.php";
           date_default_timezone_set("PRC");
                  $calendar= new Calendar;
                  $calendar->out();

    ?>











