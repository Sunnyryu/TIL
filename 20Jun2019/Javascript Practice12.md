## JavaScript

#### Practice

```html

<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>이벤트</title>
<script>
	 window.addEventListener("load", function(){
 document.querySelector("#btn1").onclick =  function(){
		var span1 = document.querySelector("#count1");		 
		span1.innerHTML=Number(span1.innerHTML)+1;		
	};
 document.querySelector("#btn2").onclick =  function(){
		var span2 = document.querySelector("#count2");
		span2.innerHTML=Number(span2.innerHTML)+1;
		document.querySelector("#btn1").onclick();//강제 이벤트 발생
	};
}, false);

</script>
</head>
<body>
 <h3> 자바스크립트 이벤트 </h3>
# 강제 이벤트 발생  방법 : 이벤트소스객체.on이벤트();<br>
<button id="btn1">Button 1</button>
<button id="btn2">Button 2</button><br>
<h3>Button 1 Click Count : <span id="count1">0</span></h3>
<h3>Button 2 Click Count : <span id="count2">0</span></h3>
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
div, h1, p { border:2px solid black;
             padding : 10px;
             margin : 10px; }
</style>
<script>
 window.addEventListener("load", function(){
	document.getElementById("outerDiv").onclick= function(evt){
			var event = evt || window.event;

		event.cancelBubble = true; // IE의 이벤트 전파를 취소

		if(event.stopPropagation){
			event.stopPropagation(0);// W3C 표준 이벤트 전파 취소

		}
		this.style.backgroundColor='gray';
	}
	document.getElementById("innerDiv").onclick= function(evt){
		var event = evt || window.event;

		event.cancelBubble = true; // IE의 이벤트 전파를 취소

		if(event.stopPropagation){
			event.stopPropagation(0);// W3C 표준 이벤트 전파 취소

		}
		this.style.backgroundColor='cyan';
	}
	document.getElementById("header1").onclick= function(evt){
		// var event = evt || window.event;
		console.dir(evt);


	

		if(event.stopPropagation){
			event.stopPropagation();// W3C 표준 이벤트 전파 취소

		}else{

		event.cancelBubble = true; // IE의 이벤트 전파를 취소
		}
		this.style.backgroundColor='magenta';

	}
	document.getElementById("p1").onclick= function(evt){		 
		var event = evt || window.event;

		event.cancelBubble = true; // IE의 이벤트 전파를 취소

		if(event.stopPropagation){
			event.stopPropagation(0);// W3C 표준 이벤트 전파 취소

		}
		this.style.backgroundColor='orange';
	}
}, false);
</script>
</head>
<body>
 <h3> 자바스크립트 버블링과 캡처링 </h3>
자바스크립트 버블링 : html문서내에서 자식 태그객체에서 발생된 이벤트가 부모 태그 객체로 이벤트 전파되는 것 <br>
자바스크립트 캡처링 : html문서내에서 부모 태그객체에서 발생된 이벤트가 자식 태그 객체로 이벤트 전파되는 것 <br>
이벤트 버블링을 막으려면 
<div id="outerDiv">
  <div id="innerDiv">
    <h1 id="header1">
       <p id="p1">이벤트 전파</p>
    </h1>
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
<script>
window.addEventListener("load", function(){
	//브라우저 기본 이벤트 핸들러 취소
	document.getElementById("searchForm").onsubmit = function(){
		// return false;
		event.preventDefault(); 
	}// data.jsp가 안넘어가짐
	document.getElementById("link1").onclick = function(){
		// return false;
		event.preventDefault(); //w3 궈장 방식
	} // google을 눌러도 안됨.
 
}, false);
</script>
</head>
<body>
 <h3> 브라우저에 정의된 기본 이벤트 취소 </h3>
 브라우저에서 자동으로 처리해주는 기본 이벤트 핸들러를 취소하려면 이벤트 핸들러 함수를  override해서 false를 리턴합니다.<br>
<a id="link1" href="http://www.google.com">구글</a><br>
<form id="searchForm" action="data.jsp" method="GET">
찾기 <input type="search">
<input type="submit" value="검색">
</form>
</body>
</html>
```

```html
<!DOCTYPE html> 
<html> 
<head> 
<meta charset="utf-8" /> 
<script> 
var array = new Array("sunny", "jay", "kjk", "kimc", "jenny", "rooney", "kevin", "ray", "soo","robert"); 
function grabname(){ 
  document.getElementById("뽑기").innerHTML		= (array[Math.floor(Math.random()*array.length)]); 
} 


setInterval(function(){ grabname(); }, 2000); 
</script> 
</head> 
<body> 
<h3>당신의 운은?</h3>
<div id="뽑기"></div> 
</body> 
</html> 
```







