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
동일한 속성을 가지는 객체를 하나 이상 생성해야 할 경우 객체 리터럴 방식보다는 생성자 함수를 정의하고, 생성자 함수로부터 property값만 전달해서 객체 생성을 권장합니다.<br>

<script>
var student = {이름 : '홍길동', 
	영어:88, 	
	국어:90, 
	수학:77, 
	과학:75,
total: function(){  //총점 변환

	return this.영어+this.수학+this.국어+this.과학
},
average : function(){   //평균 변환
	return this.total()/4;
}
}
document.write(student.이름+"의 총점 :"+ student.total()+"<br>");
document.write(student.이름+"의 평균 :"+ student.average()+ "<br>")

</script>

<script>

/*	 	var student0 = { 이름: '장기영', 국어: 87, 수학: 98, 영어: 88, 과학: 95 };
   		var student1 = { 이름: '연하진', 국어: 92, 수학: 98, 영어: 96, 과학: 98 };
        var student2 = { 이름: '구지연', 국어: 76, 수학: 96, 영어: 94, 과학: 90 };
        var student3 = { 이름: '나선주', 국어: 98, 수학: 92, 영어: 96, 과학: 92 };
        var student4 = { 이름: '윤아린', 국어: 95, 수학: 98, 영어: 98, 과학: 98 };
        var student5 = { 이름: '윤명월', 국어: 64, 수학: 88, 영어: 92, 과학: 92 };
        var student6 = { 이름: '김미화', 국어: 82, 수학: 86, 영어: 98, 과학: 88 };
        var student7 = { 이름: '김연화', 국어: 88, 수학: 74, 영어: 78, 과학: 92 };
        var student8 = { 이름: '박아현', 국어: 97, 수학: 92, 영어: 88, 과학: 95 };
        var student9 = { 이름: '서준서', 국어: 45, 수학: 52, 영어: 72, 과학: 65 };*/
// 객체를 위한 생성자 함수 정리!
        function Student(name, ko, math, en, sci){
        	this.name = name;
        	this.ko = ko;
        	this.math = math;
        	this.en = en;
        	this.sci = sci;
        	this.total = function(){
        		return this.ko+this.math+this.en+this.sci;
        	};
        	this.average = function(){
        		return this.total()/4;
        	};
        }
        //객체 생성
      var students = [new Student('장기영', 87, 98, 88, 95), new Student('연하진', 92, 98, 96, 98), new Student('구지연', 76, 96, 94, 90), new Student('나선주', 98, 92, 96, 92), new Student('윤아린', 95, 98, 96, 98), new Student('윤명월', 64, 88, 92, 92), new Student('김미화', 82, 86, 98, 88), new Student('김연화', 88, 74, 78, 92), new Student('박아현', 97, 92, 88, 95), new Student('서준서', 45, 52, 72, 65) ];
      
      for (var idx in students )
      {
      document.write(students[idx].name+"의 총점 :" + students[idx].total()+", 평균 :" + students[idx].average()+"<br>");	

      }  
//document.write(student.이름+"의 총점 :" + student.total()+"<br>");
//document.write(student.이름+"의 평균 :" + student.average()+"<br>");

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
 
생성자 함수로 생성되는 객체들의 기능은 모두 동일하므로 객체 생성시마다 메모리에 객체의 메서드가 생성되는 것보다는 <br>
생성자 함수는 function객체로 메모리에 생성될때 프로토타입 속성객체가 자동으로 생성됩니다.<br>
프로토타입 속성객체에 생성자 함수로 생성되는 객체들의 기능을 추가하면, 전역 메서드처럼 사용 가능합니다. 메모리 낭비를 줄이고..<br>


<script>
    
//객체 생성을 위한 생성자 함수 정의
   function Student(name, ko, math, en, sci ){
			this.name = name;
			this.ko= ko;
			this.math = math;
			this.en = en;
			this.sci = sci;			
	}
	Student.prototype.total= function(){//총점 반환
					return  this.en+this.math+this.ko+this.sci;
			};
	Student.prototype.average = function(){  //평균 반환
                    return this.total()/4;
			};

console.dir(Student);
//객체 생성
var students = [ new Student('장기영', 87,  98,  88,  95),
                 new Student('연하진', 92, 98, 96, 98 ),
				 new Student('구지연', 76,  96,  94, 90 ),
				 new Student('나선주', 98, 92, 96, 92),
				 new Student('윤아린', 95, 98, 98, 98 ),
				 new Student('윤명월', 64, 88,92,92),
				 new Student('김미화', 82, 86, 98,88 ),
				 new Student('김연화', 88, 74, 78, 92 ),
				 new Student('박아현', 97, 92, 88, 95),
				 new Student('서준서', 45, 52, 72, 65)
				 ];


for (var idx in students )
{
document.write(students[idx].name+"의 총점 :" + students[idx].total()
               + ", 평균 :" + students[idx].average()+"<br>");
 }

</script>
</body>
</html>

```







