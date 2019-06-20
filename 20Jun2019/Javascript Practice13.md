## JavaScript

#### Practice

```html

<!DOCTYPE html >
<html>
<head>
	<meta  charset="UTF-8">
	<title></title>
	<style>
		body{
			font-size:9pt;
		}
		#panel1{
			border:1px #000000 solid;
			line-height:400px;
			font-size:100px;
			width:400px;
			height:400px;
			text-align:center;
			vertical-align:middle;		
		}
	
	</style>
	<script>
		/*
		 	Step #8
		 		- 1에서 참여인원수 내에서 랜덤숫자 만들기(20분)
		 		
		 	Step #7
				- 출력패널 스타일 초기화
			
			Step #6-1
				- 리팩토링
					
			Step #6
				- 당첨 버튼 클릭시 램덤숫자출력정지
				- 현재 화면에 출력된 숫자가 당첨번호, 이를 부각시키기 위해서 글자색을 빨간색, 크기를 250px로 만듬.
			
	
	
			Step #5
				- 초기 시작시 랜덤숫자 만들기는 정지된 상태.
				- 시작 버튼 클릭시 랜덤하게 숫자가 출력되도록 만들기.
			
			
			Step #4
				- step #1에서 만든 숫자를 레이아웃에 출력하기.("숫자가 출력될 영역"Element를 구해야겠죠?)
			
			
			Step #3
				- 레이아웃 구성하기(숫자가 출력될 영역, 시작버튼, 당첨버튼등이 있어야 겠죠?)
			
			Math.
			Step #2
				- 0.1초에 한번씩 Random 하게 1부터 100사이의 정수 만들기.(setInterval을 이용하세요)
			
			Step #1
				- Random하게 1부터 100사이의 정수 만들기.
			
		
		*/
 var panel1;
  var nTimerID;
  var labTotal;
  var nTotalMember;
  window.onload=function(){
   this.init();// 요소 초기화 실행.   
   this.initEventListener();// 이벤트 초기화 실행. 
  }    
  function init(){// 요소 초기화.   
   this.panel1 = document.getElementById("panel1");// 숫자가 출력될 #panel1을 찾아 전역변수에 담아둡니다.
   this.nTimerID = 0;// 참여인원 정보가 입력된 패널을 찾아 전역변수에 담아둡니다.
   this.labTotal = document.getElementById("lab_total"); // 참여 인원수 입력 input 태그 하에 담아둔거
   this.nTotalMember = 0;   
  }    
  function initEventListener(){// 이벤트 초기화.
   var btnStart = document.getElementById("btn_start");
   btnStart.addEventListener("click", function(){
    startTimer();
   },false);   
   var btnStop = document.getElementById("btn_stop");
   btnStop.addEventListener("click",function(){
    stopTimer();
   },false);   
  }  
  function startTimer(){  
   if(this.nTimerID==0){    
    this.nTotalMember = Number(this.labTotal.value);//입력된 참여인원수를 구해옵니다.    
    this.resetPanel1Style();// 타이머 시작시 #panel1의 글자색을 초기화 시켜 줍니다.   
    this.nTimerID = setInterval(this.createNumber,200);// 0.2초에 한번씩 createNumber()함수를 실행시켜 줍니다.
   }
  }    
  function stopTimer(){
   if(this.nTimerID){
    clearInterval(this.nTimerID);// createNumber()함수 호출하는 타이머를 멈춥니다.
    this.nTimerID = 0;    
    this.showchange();//출력효과 추가.
   }
  }    
  function createNumber(){ 
   var nNum = 1+Math.floor(Math.random()*this.nTotalMember);// 랜덤하게 1에서 참여인원수 사이의 숫자를 만들어 냅니다.   
   this.panel1.innerHTML = nNum;//만들어진 숫자를 innerHTML에 대입시켜 줍니다.   
   this.panel1.style.fontSize = 100+(Math.random()*150)+"px";// 폰트 크기를 100~250으로 랜덤하게 설정해줍니다.
  }     
  function showchange(){ // 출력효과 추가.  
   this.panel1.style.color = "red";// 당첨자를 알리기 위해서 #panel1의 글자색과 크기를 변경시켜줍니다. 
   this.panel1.style.fontSize = "250px"; 
  }    
  function resetPanel1Style(){
   this.panel1.style.color = "#000000";// 출력패널의 스타일을 초기화 시켜준다. 
  }

	</script>
</head>

<body>
	<div> 
		<h4>경품추첨기-ver 0.1</h4>
	
		<div id="panel1" > 1
			<!-- 이곳에 숫자가 출력됩니다. -->
		</div>
	
		<div id="nav">
			참여인원 : <input type="text" id="lab_total" value="100">
			<button id="btn_start">시작</button>
			<button id="btn_stop">멈춤</button>
		</div>
	</div>
</body>
</html>
```

```html

<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>이벤트</title>
<style>
 
</style>
<script>
window.addEventListener("load", function(){
	var panel = document.getElementById("panel");
    var nNum = 1+Math.floor(Math.random()*100);			
	panel.innerHTML = nNum;			
	panel.style.fontSize = 100+(Math.random()*100)+"px";    
	setTimeout(function(){
		//location.href="http://www.w3schools.com";
		//location.assign("http://www.naver.com");
		//lcation.replace("http://www.daum.net");
		location.reload();
		//location.href=location.href;
		}, 3000);
	}, false);
  
</script>
</head>
<body>
<!-- <h3> 이 페이지는 3초 후에 www.w3schools.com으로 이동합니다. </h3> -->
<h3> 이 페이지는 3초 후에 reload됩니다. </h3>
 <div id="panel">
	
 </div>
</body>
</html>

```

```html
<!DOCTYPE html  >
<html>
<head>
	<meta  charset="UTF-8">
	<title></title>
	<style>
		body{
			font-size:9pt;		
		}
		
		#panel{
			width:600px;
			height:300px;
			border:1px solid #999;
			position:relative;
		}
		
		#bar{
			position:absolute;
			left:50px;
			top:190px;
			width:500px;
			height:20px;
			
			background:#F30;
		}
		
		#img1{
			position:absolute;
			left:50px;
			top:120px;		
		}
		
		#nav{
			text-align:center;
			width:600px;
		}
	</style>
	
	<script>
		var nEndX;
		var nCurrentX;
		var nStartX;
		var nTimerID;
		var nStep;
		var objIMG;
	
		window.onload=function(){
			var objBar = document.getElementById("bar");
			
			// 시작위치 구하기.
			this.nStartX = objBar.offsetLeft;
	
			// 마지막 위치.(시작위치 + bar의 넓이 - 이미지 넓이)
			this.nEndX = objBar.clientWidth;
			this.nEndX += this.nStartX;		
			this.nEndX -= 128;
	
			// 이미지의 현재 위치를 시작위치로 설정.
			this.nCurrentX = this.nStartX;
			
			this.nStep = 2;
			this.nTimerID = 0;
			
			// 계속해서 사용하게 될 이미지 엘리먼트를 변수에 저장.
			this.objIMG = document.getElementById("img1");
		 
			// 시작버튼 이벤트 리스너 등록.
			document.getElementById("btn_start").addEventListener("click",function(){
				start();
			},false);
			
			// 정지버튼 이벤트 리스너 등록.
			document.getElementById("btn_stop").addEventListener("click",function(){
				stopMove();
			},false);
		}
		 
		
		// 타이머 실행.
		function start(){
			if(this.nTimerID==0)
				this.nTimerID = setInterval(this.startMove,30);
			
		}
		
		// 이미지 움직이기.
		function startMove(){
			// nStep만큼 이동합니다.
			this.nCurrentX += this.nStep;
			
			//  위치값이 마지막 위치값을 넘어가는 순간, 
			//  시작 위치<--- 마지막 위치로 이동될수 있도록 방향을 바꿔준다.
			if(this.nCurrentX>this.nEndX){
				this.nCurrentX=this.nEndX;
				this.nStep=-2;
			}
			// 위치값이 시작위치값을 넘어가는 순간,
			// 시작위치 ---->마지막 위치로 이동될수 있도록 방향을 바꿔준다.
			if(this.nCurrentX<this.nStartX){
				this.nCurrentX=this.nStartX;
				this.nStep=2;
			}
			
			// 최종적으로 조절된 위치값을 left에 적용시켜 준다.
			this.objIMG.style.left=this.nCurrentX+"px";		
		}
		
		// 타이머 정지시키기.
		function stopMove(){
			if(this.nTimerID!=0){
				clearInterval(this.nTimerID);
				this.nTimerID=0;
			}
		}
	</script>
</head>

	<div> 
		<h4>#img1을 #bar의 영역에서 계속 좌우로 움직이도록 만들어주세요.</h4>
		<div id="panel">
			<div id="bar"> </div>
			<div id="img1">
				<img src="fish.png">
			</div>
		</div>
		<div id="nav">
			<button id="btn_start">시작</button>
			<button id="btn_stop">멈춤</button>
		</div>
	</div>       
</body>
</html>

```









