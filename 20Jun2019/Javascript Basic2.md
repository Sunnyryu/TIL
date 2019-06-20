## JavaScript

#### 복습



##### javascript





- 자바스크립트 함수를 정의하는 방법 
  
  - 함수 선언문으로 정의
    - function square(x) { return x*x ;}
  - 함수 리터럴(익명 함수)로 정의
    - var square = function(x) { retunrnx*x ; }
    - sqaure(5); // 호출(변수에 할당)
  - Function 생성자를 사용해서 정의
    - var square = new Function("x", "return x*x");
    - sqaure(5); // 호출(변수에 할당)
  - 화살표 함수 표현식(람다식 ~~)으로 정의
    - var square = x => x*x (return 생략 가능)
    - sqaure(5); // 호출(변수에 할당)
  
  ```html
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="utf-8">
  <title>Review</title>
  	<!-- <script>
  		window.onload = function(){
    		this.
    }
    button.onclock = function(){
    	this...
    }
  	</script> -->
  </head>
  <body>
  <script>
     function square(x) {  return x*x ; }
     console.log( square(5));
     var square1  = function(x) { return x*x; }
     console.log(square1(5)); //호출
   
    var square2  = new Function("x", "return x*x");
    console.log(square2(5)); //호출
   
    var square3  = x => x*x;
     console.log(square3(5)); //호출
  
    console.log( (function(x) { return x*x })(5));
    console.log(this);  //Window
    console.log(this==window);
  
    function f(){ console.log(this);} //전역 유효 범위의 namespace 에 추가되므로 
    f(); //this는 window입니다.
  
  
    function makeCounter(){
    	var count = 0;
    	return g;
    	function g(){// 클로져함수
    		return count++;
    	}
    }
    var counter = makeCounter(); // 함수 수행이 끝나면 Garbage collect되어야 하지만 클로져 함수를 리턴하는 함수의 실행 Context는 메모리 속에 남아 있음.(counter 변수를 사용하고 있기 떄문)
    console.log(counter()); // 함수가 끝나도 garbage Collection 되지 못하고 남아있음
    console.log(counter());
    console.log(counter());
  
  </script>
  <script>
  function fact(n){
      if(n<=1) return n;
      return n*fact(n-1);
  }
  console.log(fact(5));
  </script>
  </body>
  </html>xxxxxxxxxx <script> function square(x) {  return x*x ; }   console.log( square(5));   var square1  = function(x) { return x*x; }   console.log(square1(5)); //호출   var square2  = new Function("x", "return x*x");  console.log(square2(5)); //호출   var square3  = x => x*x;   console.log(square3(5)); //호출  console.log( (function(x) { return x*x })(5));  console.log(this);  console.log(this==window);​ </script><!DOCTYPE html><html><head><meta charset="utf-8"><title>Review</title>    <!-- <script>        window.onload = function(){        this.  }  button.onclock = function(){    this...  }    </script> --></head><body><script>   function square(x) {  return x*x ; }   console.log( square(5));   var square1  = function(x) { return x*x; }   console.log(square1(5)); //호출   var square2  = new Function("x", "return x*x");  console.log(square2(5)); //호출   var square3  = x => x*x;   console.log(square3(5)); //호출​  console.log( (function(x) { return x*x })(5));  console.log(this);  //Window  console.log(this==window);​  function f(){ console.log(this);} //전역 유효 범위의 namespace 에 추가되므로   f(); //this는 window입니다.​​  function makeCounter(){    var count = 0;    return g;    function g(){// 클로져함수        return count++;    }  }  var counter = makeCounter(); // 함수 수행이 끝나면 Garbage collect되어야 하지만 클로져 함수를 리턴하는 함수의 실행 Context는 메모리 속에 남아 있음.(counter 변수를 사용하고 있기 떄문)  console.log(counter()); // 함수가 끝나도 garbage Collection 되지 못하고 남아있음  console.log(counter());  console.log(counter());​</script><script>function fact(n){    if(n<=1) return n;    return n*fact(n-1);​ }fact(5);</script></body></html>html
  ```
  
- 즉시 실행 함수 - 익명 함수를 정의하고 바로 실행하는 함수 한번 실행하므로 초기화 작업할 때 사용함(1번 2번은 전역객체에 추가되며, 3번은 전역 유효 범위는 window 객체 임)

  - (function(x) {return x*x})(5);
  - (function(x) {return x*x}(5);
  - (function square(x) { return x*x})(5);

- 모든 함수의 인수는 가변 길이를 가집니다.

  - 선언된 인수보다 적으면 인수를 참조할 떄 undefined
  - 선언된 인수보다 많으면 무시
  - 모든 함수의 생성될 때에 전달되는 함수의 저장되는 property는 Arguments라는 객체의 arguments입니다.
    - arguments.length, arguments[index]로 꺼냄..
  - 자바스크립트에서 factorial로 계산하려면 재귀함수로 만들고(정의하고) 사용할 수 있음.

```html
<script>
function fact(n){
    if(n<=1) return n;
    return n*fact(n-1);
 
}
fact(5);
</script>
```

- 함수가 호출되어 실행되는 시점에 this 값이 결정됨.
  - 최상위 레벨의 코드에서 this는 Window 객체의 참조변수 window
  - 이벤트 헨들러 함수 내부에서 this는 이벤트 소스 객체
    - window.onload(load 이벤트가 발생했을 때 여기에 함수를 정의하는 것!)
  - 생성자 함수 안에서 this는 생성자 함수로부터 생성되는 객체 자신임..
  - 호출된 함수 내부에서 this는 window입니다.

- 객체 정의 방법 :

  - 객체 리터럴로 정의

    {속성 : 값, 속성: 값, 속성:function(){}...}

  - 생성자 함수를 정의하고 생성자 함수로부터 객체 생성할 수 있습니다.

```
- function Person(name, age){

  var _name = name; // 로컬변수는 외부에서 참조 불가능함(private 성격을 가짐)

var _age = age;
    return {
        getName : function() { return _name; },
	getAge : function() { return _age; },
	setAge : function(n ) {_age =n; }
    };
}

var p = new Person("kim" , 30);
//console.log(p._name) ;//오류
//console.log(p._age) ;//오류
console.log(p.getName()) ; 
console.log(p.getAge()) ; 
```

- 함수적 프로그래밍 특성

  - 변수에 함수를 저장할 수 있음.
  - 배열의 요소로도 함수를 저장할 수 있음
  - 함수 내부에 함수를 정의할 수 있음. (nested function)
  - 함수에서 함수를 반환할 수 있음.
    - (용어)내부에 함수를 정의하거나 함수를 반환하는 함수를 고차 함수라고 함.
  - 함수의 인수로 함수를 전달할 수 있음.
    - (용어)인수를 전달되는 함수를 콜백함수라고 함.

- 자바 스크립트 객체 분류

  - 내장 객체 - Object, String, Boolean, Number, Array(매우 유용함)

  - 브라우저 객체 - window

    - window - close(), open(url, name, {optional 하게 쓰임}, moveBy(), moveTo(), alert(), confirm(), prompt(), setTimeout(function(){}, timeout time(ex :5000)), clearTimeout(id) - 시간이 경과되기 전에 종료를 할 수 있음), setInterval(function(){}, time - id값을 리턴하며 일정한 시간에 조건값을 나타내줌) , clearInterval(id)

    - window 객체의 속성 document는 Document로서 HTML요소관련 처리 객체

    - Document - getElementById("문자열"), getElementsByName("문자열"), getElementsByTagname("문자열"), getElementsByClassName(), querySelector("css의 select 형식") - 최초의 css 형식을 가져올 수 있음, querySelectorAll("css의 select 형식") - css의 형식을 모두 가져올 수 있음, createElement()  - 새로운 것을 만들기 위해, createComment() - 주석 추가, createDocumentFragment(), createAttribute(), createTextNode() - 내용에 대한 text, 

      setAttribute() , getAttribute(), removeAttribute(),

      parentNode - 부모님 속성을 가져옴, childNode - 자식의 속성을 가져옴

      body, appendChild() 

    

    

  - ECMAScript 객체









