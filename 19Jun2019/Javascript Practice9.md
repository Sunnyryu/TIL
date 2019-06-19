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
<h3>내장 객체</h3>
 



<script>
console.dir(Date);
	// var today = new Date();
	// for(var key in today){
	// 	document.write("*"+key+":"+today[key]+"<br>");
	// }

	var array1 = new Array();
	var array2 = new Array(10);
	var array3 = new Array(10, 20, 30, 40,50);
	document.write("* array1.length :"+array1.length+"<br>");
	document.write("* array2.length :"+array2.length+"<br>");
	document.write("* array3.length :"+array3.length+"<br>");
	array3[5] = 60;
	array3.push(70);
	for (var idx in array3)
	{
		document.write("* array3[idx]="+array3[idx]+"<br>");
	}
	delete array3[1];
	for (var idx in array3)
	{
		document.write("* array3[idx]="+array3[idx]+"<br>");
	}
</script>
자바스크립트에서 배열은 서로 다른 타입의 요소를 저장할 수 있고<br>
동적으로 요소를 추가하거나 삭제할 수 있습니다.
</body>
</html>


```

```html

<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title></title>
<script> 
window.onload = function(){
	var btn = document.getElementById("newOpen");
	btn.onclick = function(){
		window.open("19_12.html", "", "width=300 height=300");
	}	
} 
</script>
</head>
<body>
<h3>Window 객체 활용</h3>
<button id="newOpen"> 새창 열기</button> <br>
	 
</body>
</html>

```

```html

<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title></title>
<script> 
window.onload = function(){
	document.getElementById("up").onclick = function(){
		window.moveBy(0,-10);
	};
	document.getElementById("left").onclick = function(){
		window.moveBy(-10,0);
	}; 
	document.getElementById("right").onclick = function(){
		window.moveBy(10,0);
	};
	document.getElementById("down").onclick = function(){
		window.moveBy(0,10);
	};	
} 
</script>
</head>
<body>
<h3>19_11.html</h3>
<input type="button" id="up" value="    UP   "   /> <br />
<input type="button" id="left" value="  LEFT  "    />     
<input type="button"  id="right"value=" RIGHT "    /> <br /> 
<input type="button" id="down" value=" DOWN "    /> 
	 
</body>
</html>

```

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title></title>
<script>
	
window.onload = function(){	 
	var cnt = 0;	
	var intervalID = setInterval(function(){
		document.write(++cnt+"<br>");
	}, 1000);
	
	setTimeout(function(){
		clearInterval(intervalID);
	}, 10100);

} 

	
</script>
</head>
<body>
<h3>1초마다 숫자 출력하고 10까지 출력 후 window 종료</h3>
</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title></title>
<script>
	window.onload = function(){
		setTimeout(function(){
			window.close();
		},5000);
	}
</script>
</head>
<body>
<h3>5초 후에 window창 종료가 됌.</h3>
</body>
</html>
```







