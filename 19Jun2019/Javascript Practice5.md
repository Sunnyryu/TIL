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
<h3>객체 리터럴 방식으로 객체 생성</h3>

<script>
var employee = {}; // 빈 객체 생성, var emp = new Object(); 
employee.ename = 'scott';
employee.job = 'developer';
employee.salary = 5000;
employee.hiredate = '2013/01/01';
employee.address = '삼성동';

document.write("employee.ename="+employee.ename+"<br>");
document.write("employee['job']="+employee["job"]+"<br>");
document.write("<br>");

for(var key in employee){//key변수에는 객체의 property가 저장됨.
	document.write(key +":"+employee[key]+"<br>");
}
document.write("employee instanceof Object =>"+(employee instanceof Object)+"<br>");
// Object 상속 확인 (대상 객체(Math, String, Number) 중 최상위 Object 상속 확인)

console.dir(Object);
document.write(employee+"<br>");
employee.toString = function(){
	var output = "";
	for(var key in this){
		if(key != 'toString'){
			output+=key=" : "+this[key]+"\n";
		}
	}
	return output;
}
document.write(employee+"<br>");
// document.write(employee.toString()+"<br>")
delete(employee.address);
document.write(employee+"<br>");
document.write("address in employee" + ('address' in employee)+"<br>");
document.write("hiredate in employee" + ('hiredate' in employee)+"<br>");
</script>

</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
<h3>객체 리터럴 방식으로 객체 생성</h3>
# for in 반복문을 객체의 속성에 접근할 때 사용가능<br>
# 객체에 대해서 사용하는 in 키워드는 속성 존재 여부를 체크할 때 사용할 수 있습니다.<br>
# 객체의 속성을 객체, 속성 대신 속성명으로만 사용할 때 with(객체){} 사용<br>
# 객체 리터럴 방식으로 정의되는 객체는 동적으로 속성, 메소드를 추가하거나, 제거할 수 있습니다.<br>
<script>
var student = {이름 : '홍길동', 영어:88, 국어:90, 수학:77, 과학:75};
document.write(student.이름+"의 총점 :"+(student.영어+student.국어+student.수학+student.과학)+"<br>");
with(student){
	document.write(이름+"의 평균:" +(영어+국어+수학+과학)/4+"<br>");
}
</script>

</body>
</html>
```







