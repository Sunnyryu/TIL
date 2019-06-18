## JavaScript

#### Practice

```html
<!--ex1-->
<!DOCTYPE html>
<html iang="ko">
<head>
<meta charset="utf-8">
<title>팩토리얼 계산</title>
</head>
<body>
	<script>
		function fact(n){
			if( n<= 1) return n;
			return n*fact(n-1);
		}
		for(var i =1; i<10; i++){
			console.log(i + "! = " + fact(i));
		}
	</script>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
<scirpt>
	window.alert("head: 태그내에 포함된 javascript 실행");
</scirpt>
</head>
<body>
	<script>
	alert("body 태그내에 포함된 javascript실행");
</script>
</body>
</html>
```

```html
<!--ex2-->
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
<script>
	var msg = document.getElementById("div1").innerHTML;
	window.alert(msg);
</script>

</head>
<body>
<div id="div1">
	body 태그 내에 div tag입니다.
</div>
</body>
</html>

<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
<script src="./first.js"></script>

</head>
<body>
외부 javascript파일을 로딩해서 실행합니다. 
</body>
</html>
```





