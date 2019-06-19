## JavaScript

#### Practice

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>자바스크립트 함수</title>
</head>
<body>
<h3>자바스크립트 함수</h3>
함수 내부에 함수를 정의할 수 있음. => 외부함수와 충돌이 발생되는 경우, 함수를 사용하는 내부에 정의할 수 있으며, 내부함수는 내부함수가 정희함수 내부에서만 호출할 수 있음.<br>
<script>
	/*function square(x){// 인수의 제곱을 반환
		return x*x;
	}*/
	function pythagoras(width, height){ //직각삼각형의 빗변의 길이
		function square(x){
			return x*x;
		}

		return Math.sqrt(square(width)+square(height));
	}
	document.write("밑변3, 높이4인 삼각형의 빗변의 길이 :" +pythagoras(3,4)+"<br>");




	function square(width, height, hypotenuse){
		if(width * width + height * height == hypotenuse * hypotenuse){
			return true;
	}
		
	else{
		return false;
	
	}
	document.write("a:"+sqaure(3,4,5)+"<br>");
}
</script>
</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>자바스크립트 함수</title>
</head>
<body>
<h3>자바스크립트 함수</h3>
함수를 매개변수로 전달하고, 함수를 리턴하는 함수를 정의 가능 <br>
var 키워드를 생략한 함수 내부에 선언된 변수는 함수호출후에 전역변수로 
Global 실행 컨텍스트에 생성됩니다. 함수외부에서 참조가 가능해집니다.<br>
<script>
 var globalVar = 'korea';//전역변수 
  function test(name){
	  globalVar2 = name; //var 키워드를 생략한 함수 내부에 선언된 변수는 함수호출후에 전역변수로 Global 실행 컨텍스트에 생성됩니다. 함수외부에서 참조가 가능해집니다.
	  var localVar = "Hello~"+name+"!!"; //로컬변수
	  return function(){
		       return localVar;
	  }
  }

	document.write("전역변수 globalVar :"+ globalVar+"<br>");
	// document.write("전역변수 globalVar2 :"+ globalVar2+"<br>");
	test('독도');//함수 호출 후
	document.write("전역변수 globalVar2 :"+ globalVar2+"<br>");
	// document.write("지역변수 localVar :"+ localVar+"<br>");
	document.write("지역변수 localVar를 클로저 함수를 통해 참조 가능");
	test(('제주도')+"<br>");

	function caller(callee){
		for(var i=0;i<5;i++){
			callee();
		}
	}
	function callee(){
		alert("callee");
	}

  caller(callee);
</script>
#let은 블록 유효 범위를 갖는 자연변수 선언<br>
#constr는 블록 유효 범위를 갖는 상수 선언<br>
<script>
	let x = "outer x";
	{	
		let x = "inner x";
		let y = "inner y";
		document.write("블럭 내부에서 x :"+x+"<br>");
		document.write("블럭 내부에서 y :"+y+"<br>");
	}
	document.write("블럭 외부에서 x :"+x+"<br>");
	// document.write("블럭 외부에서 y :"+y+"<br>");
	{	
		const c = 3;
		document.write("블럭 내부에서 c :"+c+"<br>");
		// c= 5; //TypeError
	}



</script>
</body>
</html>

```







