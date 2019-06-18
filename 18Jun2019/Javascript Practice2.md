## JavaScript

#### Practice

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
#자바스크립트에서 변수선언은 var 변수명;<br>
var 변수명 = 초기값; <br>
자바 스크립트에서 문자열은 "" 또는 ''로 감싸줘야 합니다<br>
변수만 선언하고 초기화하지 않으면, 아직 메모리에 생성이 되지 않은 상태이므로<br>
자바 스크립트가 사용하는 브라우저 프로그램의 메모리에서 a변수와 sum변수로 저장된 값이 없으므로 undefined라고 결과가 출력됨.<br>
<script>
	var sum, a;//변수 선언..
	console.log("a="+a);// a는 ~~~ 출력
	document.write("sum"+sum+"<br>"); // 결과 출력
	
	console.dir(window);//함수 외부에서 선언된 것은 자동으로 윈도우(전역속성) 객체로 추가함..
	// document.write("x="+x+"<br>"); // 변수가 지정되지 않아 x는 값이 나오지 않습니다.
	// y=3 // 실행시에 전역객체(golbal object는 window객체의 속성으로 추가됩니다.
	// document.write("y="+y+"<br>");
	korea=3;
	document.write("korea="+korea+"<br>");
	var a= 5; // javascript에서 중복선언은 오류가 발생하지 않고 마지막 선언 된 것만 남음.
	
</script>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
</head>
<body>
#자바스크립트의 데이터 유형<br>
string, number, boolean, function,  object 대소문자 구분함, 자바스크립트에서는 배열은 객체입니다.<br>
primitive type - string, number, boolean, undefined, null<br>
객체(reference type)- function, object<br>
새미콜론을 안써도 에러 발생x, 가독성에 좋을 뿐임.<br>
<script>
	var a = 1; // 정수 , 실수 구분 check (아래의 경우는 모두 number 타입)
	document.write("a변수의 타입:"+typeof(a)+"<br>");
	var b = 0.5;
	document.write("b변수의 타입:"+typeof(b)+"<br>");
	a="javascirpt";// "", ''든 모두 String 타입으로 나옴
	document.write("a변수의 타입:"+typeof(a)+"<br>");
	b='ECMAScript6';// 동적타입 언어!
	document.write("b변수의 타입:"+typeof(b)+"<br>");
	a= function(){}
	document.write("a변수의 타입:"+typeof(a)+"<br>");
	b= [];
	document.write("b변수의 타입:"+typeof(b)+"<br>");
	a= {}; //jsson(Javascript Object notation) 객체
	document.write("a변수의 타입:"+typeof(a)+"<br>");
	b= new Object();
	document.write("b변수의 타입:"+typeof(b)+"<br>");
	a= true
	document.write("a변수의 타입:"+typeof(a)+"<br>");
	a= 0x2a, b=0o73, c=0b101;
	document.write("a:"+a+"b:"+b+"c:"+c+"<br>");
	a= 1.161425E-11;
	document.write("a:"+a+"<br>");
	a='"Javascript"';
	document.write("a:"+a+"<br>");
	var c = [];
	document.write(c[0] +"<br>");//없는 배열의 요소를 읽으면 undefined 출력
	a= function(){}
	document.write("a:"+a()+"<br>");// a로 하면 a:function(){}으로 출력됨. 그런데 우리가 구해야하는 것은 a()이므로 출력하면 a:undefined로 나옴
	
	// a = function(d){
	// alert(d); // undefined로 나옵니다. 함수를 호출했을 때 전달받지 못한 인수의 값;
	// };
	// a();
</script>

</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>javascript 연산자</title>

</head>
<body>
<h3>자바스크립트 연산자</h3>

<script>
	a=1
	b=++a;
	console.log("b="+b);
	console.log("a="+a);
	c=a++ +2;
	console.log("c="+c);
	console.log("a="+a);
	// console.log("a="+(a++)++);
</script>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<script>
		var num = Math.round(Math.random()*5)+1;
		document.write("주사위의 숫자"+"<br>"+num+"<br>");
		document.write("1 + {} :" +num+"<br>");
		document.write("true + (new Date()) :"+(true + (new Date()))+"<br>");
		var msgObj = new String("Everythig is practice");
		document.write("msgObj.length :"+msgObj.length+"<br>");
		document.write("msgObj.charAt(3) :"+msgObj.charAt(3)+"<br>");
		document.write("msgObj.substring(7, 10) :"+msgObj.substring(7,10)+"<br>");
		document.write("msgObj.slice(7, 10) :"+msgObj.slice(7, 10)+ "<br>");
		document.write("msgObj.slice(-3) :"+msgObj.slice(-3)+ "<br>");
		document.write("msgObj.slice(-9, -6) :"+msgObj.slice(-9, -6)+ "<br>");
		document.write("msgObj.indexOf('t') :"+ msgObj.indexOf("t")+"<br>");
		document.write("msgObj.indexOf('i', 10) :"+ msgObj.indexOf("i", 10)+ "<br>");
		document.write("msgObj.split('') :"+msgObj.split("")+ "<br>");
		document.write("msgObj.includes('thing') :"+ msgObj.includes("thing") +"<br>");
		document.write("charCodeAt(0):"+msgObj.charCodeAt(0)+"<br>");
		document.write("msgObj.codePointAt(0) :"+ msgObj.codePointAt(0) +"<br>");
		





	</script>

</body>
</html>
```





