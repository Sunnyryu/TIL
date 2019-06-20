## JavaScript

#### Practice

```html
<!DOCTYPE html>

<html lang="ko">
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
	<ul id="doglist">
		<li>포메라니안</li>
		<li>달마시안</li>
	</ul>
	<script>
		var doglist = document.getElementById("doglist");
		doglist.appendChild(doglist.children[0]);
		var element = document.createElement("li");
		var text = document.createTextNode("불독");
		doglist.insertBefore(element,doglist.children[1]);
		element.appendChild(text);



	</script>
</body>
</html>
```

```html
<!DOCTYPE html>

<html lang="ko">
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<style>
	.box{
		display: inline-block;
		padding: 100px;
		margin: 100px;
		margin-left: 0;
		background-color: yellow;
	}
</style>
<body>
	<div class="box" id="sec1">#sec1</div>
	<br/>
	<div class="box" id="sec2">#sec2</div>
	<br/>
	<div class="box" id="sec3">#sec3</div>
	<script>
		function getScrollTop(){
			if( window.pageYOffset !== undefined){
				return window.pageYOffset;
			}else{
				return document.documentElement.scrollTop || document.body.scrollTop;
			}
		}
		function getScrollLeft(){
			if( window.pageXOffset !== undefined){
				return window.pageXOffset;
			}else{
				return document.documentElement.scrollLeft || document.body.scrollLeft;
			}
		}
		if ('scrollRestoration' in history){
			history.scrollRestoration = 'manual';
		}
		var element = document.getElementById("sec3");
		var rect = element.getBoundingClientRect();
		scroll(rect.left + getScrollLeft(), rect.top + getScrollTop());
	</script>
</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>폼 태그</title>
<script>
 function whenSubmit(){
 	//변수 선언
 	var pass = document.getElementById('pass').value;
 	var pass_check = document.getElementById('pass_check').value;
 	//비밀번호가 같은지 check
 	if (pass == pass_check){
 		alert('성공');

 	}else{
 		alert('재입력');
 		return false;
 	}
 }
</script>
</head>
<body>
<form id="my_form" action = 'data.jsp' onsubmit="return whenSubmit()">
        <label for="name">이름</label><br/>
        <input type="text" name="name" id="name"/><br/>
        <label for="pass">비밀번호</label><br/>
        <input type="password" name="pass" id="pass"/><br/>
        <label for="pass_check">비밀번호 확인</label><br/>
        <input type="password" id="pass_check"/><br/>
        <input type="submit" value="제출"/>
    </form>

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
	 // window.onload = function(){
	 // 	alert("load event handler1");
	 // }
	 // window.onload = function(){
	 // 	alert("load event handler2");
	 // }
	 // window.onload = function(){
	 // 	alert("load event handler3");
	 // }
	  // window.addEventListener("load", function(){
	 	// alert("load event handler1");}, false);
	  //   window.addEventListener("load", function(){
	 	// alert("load event handler2");}, false);
	 	//   window.addEventListener("load", function(){
	 	// alert("load event handler3");}, false); // 여러개 띄울 떄 사용함
	 window.addEventListener("load", function(){
	  var h3 = document.querySelector("#evt");	 
	  h3.onclick =function(){
		   alert("까꿍");
		   //h3.onclick =null;
		  this.onclick = null;
	 } ; 
	 document.querySelector("#evt2").onclick = function(){
	   this.style.color = 'blue';
	   this.style.backgroundColor = 'orange';
	};

}, false);

	 
	 

	 
	</script>
	</head>
	<body>
	<h3>자바스크립트 이벤트</h3>
	# DOM Level 0 이벤트 모델 : on 이벤트명 = function(){} = > 이벤트 당 하나의 이벤트 핸들러만 연결<br>
	# DOM Level 2 이벤트 모델 : 이벤트 소스에 해당하는 태그 객체(태그객체).addEventListener("이벤트명", function(){}, 이벤트캡처여부) - 기본값(default값)은 false 입니다.<br>
	이벤트당 하나 이상의 이벤트 핸들러를 연결
	<br>
	이벤트에 대한 이벤트 핸들러가 한번만 수행후 이벤트 핸들러 취소하려면 : 이벤트 소스.on이벤트 속성 = null;<br>
	<h3 id="evt">이벤트 핸들러 한번만</h3> <!-- 이것을 누르면 alert가 뜸--> 
	<h3 id="evt2"> 클릭이벤트 가 발생하면 배경색은 오렌지색, 글자색상은 파란색으로 변경하는 핸들러 실행</h3>
		 이벤트에 대한 이벤트 핸들러가 한번만 수행후 이벤트 핸들러 취소하려면 : 이벤트 소스.on이벤트 속성 =null;<br>
	이벤트 핸들러 함수 내부에서 이벤트 객체의 속성들을 핸들링할때 이벤트 소스 객체를 this 참조합니다<br>

	</body>
	</html>
```







