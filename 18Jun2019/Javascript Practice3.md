## JavaScript

#### Practice

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<script>
	
		document.write("null == undefined :"+(null == undefined)+"<br>");
		document.write("1 == '1' : "+ (1 == '1')+"<br>");
		document.write("255 == '0xff' : "+ (255 == '0xff')+"<br>");
		document.write("true == 1 : "+ (true == 1)+"<br>");
		document.write("true == '1' : "+ (true == '1')+"<br>");
		document.write("new String('a')== 'a':"+(new String('a')=='a')+"<br>");
		document.write("new Number(2) == 2:"+(new Number(2)==2)+"<br>");
		//==은 값만 비교합니다. 자바스크립트 엔진에서 자동 형변환이 수행됨.

		document.write("null === undefined:" + (null === undefined)+"<br>");
		document.write("1 === '1':" + (1 === '1')+"<br>");
		document.write("255 === '0xff' : "+ (255 === '0xff')+"<br>");
		document.write("true === 1 : "+ (true === 1)+"<br>");
		document.write("true === '1' : "+ (true === '1')+"<br>");
		document.write("new String('a')=== 'a':"+(new String('a')==='a')+"<br>");
		document.write("new Number(2) === 2:"+(new Number(2)===2)+"<br>");
		//===연산자는 값과 타입을 비교합니다.

		document.write("10>20>30 :" + (10>20>30)+"<br>");
		var a ="window.alert('eval은 문자열을 자바스크립트 코드로 실행합니다')";
		eval(a);

		var student = { "name":"kim", "ko":85, "en":90, "math":80};
		document.write("typeof(student) :"+typeof(student)+"<br>");
		document.write("typeof(student instanceof Object) :"+(student instanceof Object)+"<br>");


		document.write("ko in student :"+ ('ko' in student)+"<br>");

		var n = 26;
		document.write(n.toString()+"<br>");
		document.write(n.toString(2)+"<br>");
		document.write(n.toString(16)+"<br>");
		document.write((26).toString(16)+"<br>");

		var x =1234.567;
		document.write(x.toString()+"<br>");
		document.write(x.toString(16)+"<br>");
		document.write(x.toFixed(0)+"<br>");
		document.write(x.toFixed(2)+"<br>");
		document.write(x.toFixed(4)+"<br>");
		document.write(x.toExponential(3)+"<br>");
		document.write(x.toPrecision(3)+"<br>");
		document.write(x.toPrecision(6)+"<br>");

		document.write(String(26)+"<br>");
		document.write(String(1234567)+"<br>");
		document.write(String(0x1a)+"<br>");
		window.parseInt("123a")
		window.parseFloat("0.123b")
		Number("123a")
		document.write(window.parseInt("123a")+"<br>");
		document.write(window.parseFloat("0.123b")+"<br>");
		document.write(Number("123a")+"<br>");
		document.write(String("ABC")+"<br>"); 

document.write(window.parseInt("123a")+"<br>");
document.write(window.parseFloat("0.123b")+"<br>");
 
		document.write(String(true)+"<br>");
		document.write(String(false)+"<br>");
		document.write(String(NaN)+"<br>");
		document.write(String(null)+"<br>");
		document.write(String(undefined)+"<br>");
		document.write(String({x:1, y:2})+"<br>");	
		document.write(String([1 ,2 ,3])+"<br>");

		var s = "2"
		document.write((s - 0)+"<br>");
		document.write((+s)+"<br>");

		document.write(parseInt("3.14")+"<br>");
		document.write(parseFloat("3.14")+"<br>");
		document.write(parseInt("3.14 meters"+"<br>"));
		document.write(parseFloat("3.14 meters"+"<br>"));
		document.write(parseInt("0xff"+"<br>"));
		document.write(parseInt("0.5"+"<br>"));
		document.write(parseInt(".5"+"<br>"));
		document.write(parseInt("abc"+"<br>"));
		document.write(parseFloat("\100"+"<br>"));

		document.write(parseInt("101", 2)+"<br>");
		document.write(parseInt("ff", 16)+"<br>");

		document.write(Number("2.71828")+"<br>");
		document.write(Number(123)+"<br>");
		document.write(Number(true)+"<br>");
		document.write(Number(false)+"<br>");
		document.write(Number(NaN)+"<br>");
		document.write(Number(undefined)+"<br>");
		document.write(Number(null)+"<br>");
		document.write(Number({x:1, y:2})+"<br>");
		document.write(Number([1.2,3])+"<br>");

		//논리값으로 형변환 : !!값 또는 boolean(값);
		document.write("<br>"+(!!x)+"<br>");
		document.write(!!" "+"<br>");  
		document.write(!!null+"<br>");   
		document.write(!!undefined+"<br>"); 
		document.write(!!NaN+"<br>");
		document.write(!!""+"<br>");   
```







