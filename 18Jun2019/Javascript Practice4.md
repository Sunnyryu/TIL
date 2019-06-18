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
		var input1 = window.prompt("점수를 입력하세요", 0);
		document.write(input1+"<br>"+typeof(input1)+"<hr>");//문자열로 나옴
		var input2 = window.confirm("종료하시나요?");
		document.write(input2+"<br>"+typeof(input2)+"<br>")//boolean로 받을 때
		var input3 = Number(window.prompt("점수 입력", 0));
		document.write(input3+"<br>"+typeof(input3)+"<br>");
		var input4 = Number(window.prompt("정수 입력",0));
			if((/*parseInt(input4)*/input4)%2 ==0){
				document.write("짝수");
			}
			else{
				document.write("홀수");
			}
		var input = prompt("정수입력",0);
		var number = Number(input);
		document.write((number % 2== 0) && "짝수입니다.");
		document.write((number % 2== 0) || "홀수입니다.");


		document.write((number % 2 == 0 ? "짝수" : "홀수"));
		switch(number%2){
			case 0 :
			document.write("짝수입니다.");
			break;
			case 1 :
			document.write("홀수입니다.");
			break;
			default :
			break;
		}

		switch(number/10){
			case 10 :
			case 9 :
			document.write("A(>=90)");
			break;
			case 8 :
			document.write("B(>=80)");
			break;
			case 7 :
			document.write("c(>=70)");
			break;
			case 6 :
			document.write("d(>=60)");
			default :
			document.write("F(<60)");
			break;
		}
			
	
			
		

	
</script>

<script>
 var num= Number(window.prompt("1~100사이의 수를 입력하세요", 0));
	(num%2==0)? alert("짝수") : alert("홀수");
	
var jum= Number(window.prompt("1~100사이의 수를 입력하세요", 0));
(jum%2==0) || alert("홀수");
(jum%2==0) && alert("짝수"); 	

var jumsu = Number(window.prompt("1~100사이의 점수를 입력하세요", 0));
switch(true){
	case jumsu >89 : alert("A"); break;
	case jumsu >79 : alert("B"); break;
	case jumsu >69 : alert("C"); break;
	case jumsu >59 : alert("D"); break;
	default : alert("F"); break;
}
 
 
 </script>

</body>
</html>
```







