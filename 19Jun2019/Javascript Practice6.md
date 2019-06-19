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
# var 변수 = function(){} ; //익명(anonymous) 함수<br>
# function 이름(){ } //named function, 선언적 함수<br>
# 사용자 정의 함수는 소스가 공개되지만, 내장함수등은 소스는 native code로 공개하지 않습니다.<br>
# 변수에 저장된 익명함수는 정의된 후에 호출이 가능하지만 <br>
# 자바스크립트 엔진은 실행코드보다 먼저 선언적 함수를 읽습니다.(hoisting)<br>
#선언적 함수는 defintion전에 호출을 하더라도 실행 순서상 문제가 되지 않습니다.<br> 
<script> 
//func1();//변수에 저장된 함수 호출 - 여기서 선언하면 에러가 남..
func2(); //선언적 함수(named function) 호출
var func1 = function(){
	var jum= Number(window.prompt("1~100사이의 수를 입력하세요", 0));
	(jum%2==0)? alert("짝수") : alert("홀수");
}  
function func2(){
	var jum= Number(window.prompt("1~100사이의 수를 입력하세요", 0));
	(jum%2==0)? alert("짝수") : alert("홀수");
}
func1();
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
# 모든 함수 가변인자를 가지는 함수로 정의할 수 있습니다<br>
함수가 실행될때 실행 컨텍스트에서는 함수 내부에 arguments 배열과 유사한 타입의 속성이 생성됩니다.<br>  
arguments에 함수를 호출할때 입력값인 인수가 저장됩니다.
함수에 정의된 매개변수의 개수보다 많은 매개변수로 호출하면 실행시에 무시된다<br>
함수에 정의된 매개변수의 개수보다 적은 매개변수로 호출하면 undefined로 전달된다<br> 
<script> 

function hap(a, b){
	document.write("함수의 인수개수 :"+arguments.length+"<br>");
	var sum = 0;
	for (var item in arguments )	{
		document.write(arguments[item]+"<br>");
		sum+=arguments[item];
	}
	document.write("함수의 a, b : "+a+", "+b +"<br>");
	return sum;
}
document.write("hap(3, 5) 호출 :"+hap(3, 5) +"<br>");
document.write( "<br>");
document.write("hap(1, 3, 5, 7, 9) 호출 :"+hap(1, 3, 5, 7, 9) +"<br>");
document.write( "<br>");
document.write("hap(9) 호출 :"+hap( 9) +"<br>");	
document.write( "<br>");
var nums = [2,4,6,8,10];
document.write("hap(nums) 호출 :"+hap(nums) + "<br>"); // 배열을 인수로.. 함수로 호출
document.write("<br>");
console.dir(hap);
</script>
자바스크립트에서 배열은 모든 타입의 요소로 저장할 수 있음<br>
<script>
var arrays = [1, 'hello', true, function(){}, {name:'korea'}, [100,200]];
for (var index in arrays)
{document.write(index+":"+arrays[index]+"<br>");
}
</script>
</body>
</html>
```







