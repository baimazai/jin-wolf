# jin-wolf
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>计时</title>
	<style>
		#bg{
			width: 1000px;
			height: 800px;
			background-image: url("bg.jpg");
			margin: 0px auto;
		}
		h1{
			width: 1000px;
			color: red;
			float: left;
			text-align: center;
			font-size: 80px;
		}
		#clock{
			width: 400px;
			height: 400px;
			border-radius: 200px;
			background-color: pink;
			float: left;
			margin-left: 300px;
		}
		@font-face
		{
			font-family: myFirstFont;
			src: url("UnidreamLED.ttf");
		}
		
		#time{
			font-family: myFirstFont;
			display: block;
			width: 280px;
			height: auto;
			font-size: 100px;
			background-color: black;
			color: white;
			text-align: center;
			float: left;
			margin-left: 60px;
			margin-top: 100px;
		}
		
		#btn{
			width: 260px;
			height: 50px;
			float: left;
			margin-left: 70px;
			margin-top: 50px;
		}
		
		#begin{
			diplay: block;
			width: 80px;
			height: 50px;
			font-size: 30px;
			background-color: red;
			margin: 0px 25px;
			border-radius: 10px;
			background: linear-gradient(white,#00ffb4);
		}
		#pause{
			diplay: block;
			font-size: 30px;
			width: 80px;
			height: 50px;
			background-color: red;
			margin: 0px 20px;
			border-radius: 10px;
			background: linear-gradient(white,#00ffb4);
		}
	</style>
	<script type="text/javascript" src="jquery-3.1.1.min.js"></script>
	<script type="text/javascript">
		$(function(){
			//alert("开始吧");
			var m = 0;
			var s = 0;
			var cls = $("#time").attr("class","pause");
			m=checkTime(m);
			s=checkTime(s);
			//初始时间
			$("#time").html(m+":"+s);
			$("#begin").click(function(){
				$("#time").attr("class","run")
			});
			$("#pause").click(pause);
			//计时函数
			var t = setInterval(function(){begin()},1000);
			//开始
			function begin(){
				if($("#time").attr("class") == "pause"){
					//暂停状态
					//alert("时间停止");
					var time = $("#time").html();
					//alert(time);
					var times = time.split(":");
					//alert(times);
					m=parseInt(times[0]);
					//alert(m+1);
					s=parseInt(times[1]);
					m=checkTime(m);
					s=checkTime(s);
					//记录时间
					$("#time").html(time);
				}else if($("#time").attr("class") == "run"){
					s++;
					s=checkTime(s);
					$("#time").html(m+":"+s);
					if(s>59){
						s=0;
						m++;
						m=checkTime(m);
						$("#time").html(m+":"+s);
						if(m==10){
							//alert("到10分钟啦");
							$("#time").html("10:00");
							$("#time").html("时间到");
							clearInterval(t);
						}
					}
				}
			}
			
			//停止
			function stop(){
				clearInterval(t);
			}
			
			//暂停
			function pause(){
				$("#time").attr("class","pause");	
			}
			
			function checkTime(i){
				if(i<10){
					i = "0"+i;
				}
				return i;
			}
		});
	</script>
</head>
<body>
	<div id="bg">
		<h1>范矿公司岗位描述选拔赛</h1>
		<div id="clock">
			<span id="time" class="run"></span>
			<div id="btn">
				<input id="begin" type="button" value="开始">
				<input id="pause" type="button" value="暂停">
			</div>
		</div>
	</div>
</body>
</html>
