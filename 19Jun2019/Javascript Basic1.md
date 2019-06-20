## JavaScript

#### 복습



##### javascript



- 인터프리터 언어
- 동적 프로토타입 기반의 객체지향언어
- 동적 타입 언어
- 함수 기반 언어, 함수가 객체 => 함수형 프로그래밍 언어
  - 함수를 변수에 저장, 함수의 인수로 함수를 전달 가능! 
  - 함수에서 함수정의를 반환 가능!
- 클로저 함수





- 자바스크립트 구성 기술 요소
  - ECMScript Core
    - 브라우저에서 제공해주는 API(window = 브라우저 최상위 객체, document 객체, XMLHttpRequest(ajax 핵심 객체)....)
  - HTML5 API (Geolocation, Webworks, Canvas, Audio, Drag&Drop,....)



- 자바 스크립트 분류

  - 클라이언트 측 기술
    - (jQuery, Vue.js, React.js(서버측 기술로도 쓰이긴 함) )
  - 서버 측 기술
    - (node.js)

- java script code 작성 문법 

  - 인코딩은 utf-8 권장
  - 대소문자 구별
  -  .js 파일로 저장
  - 한 문장 단위로 ;을 구분합니다.(가독성을 위해서~~)

- 주석 처리

  - // (한줄 주석) /* */ (여러줄 주석)

- 변수 

  - 처리해야 할 값을 메모리에 저장하고 참조하기 위해 사용하는 이름!!
  - 변수 선언 키워드는 var 변수

- 변수명 naming 규칙 :

  - -, $, 영문자로 시작
  - 두분째 문자부터는 숫자도 허용
  - 길이 제한 없음(의미 있는 짧은 거 사용)
  - 키워드 x, 내장함수명 x , 내장객체명 x

- javascript 데이터 유형

  - primitive type

    - 할당 연산자를 사용하여 값을 저장
    - number, string, null, symbol, undefined, boolean

  - reference type

    - function, object, interface,.. 배열 Array는 객체 취급함(object 유형으로 나옴

    

- undefined (Yes or Not)

  - 선언 되지 않은 변수를 참조했을 때 값은 ? ReferenceError
  - 선언만 한 변수, 초기값이 할당되지 않은 변수를 참조했을 때 ? Undefined
  - 객체를 메모리에서 검색을 했는데.... 객체가 검색되지 않을 때 ? null

- javascript 출력

  - html 문서의 body 태그 영역에 출력
    - document.write()
    - document.writeln() - html에서는 작동하지 않음
  - 브라우저 또는 node 같은 자바스크립트의 실행환경에서 제공하는 콘솔창에 출력
    - console.log(), 
    - console.dir() - 내부 계층을 확인하려고 할 때
  - window.alert("메서지 출력")
    - 창으로 띄워줌 

- javascript 입력 방법 :

  - window.prompt("메세지",기본값(입력하지 않았을 때)) - 반환타입은 문자열
  - window.confirm("메세지") - 반환타입은 boolean

- javascript에서 지원하는 연산자

  - 산술연산자(*,/,%,+,-)
  - 단항연산자 (~, !, +, -(sign), ++, --)
  - 비교연산자( >, >=, <, <=, ==, !=, ===, !==)
    - ==(값만 비교), ===(값이랑 타입도 비교) 
  - 비트연산자(&, |, ^)
  - 논리연산자(&&, ||)
  - shift 연산자(<<, >>, >>>)
  - 삼항연산자(조건? 항1:항2)
    - 조건이 O면 항1 , X면 항2 반환
  - 기타연산자(typeof, in, instanceof ...)

- javascript 제어문

  - if (조건) { 문장;}

  - if(조건{

    문장; ...)else{ 문장; }

  - 다중 if문 (if 조건을 여러개 씀)

  - switch 문

    - switch(표현식){

      ​	case 값 : 문장; break; 

      default 문장; break;}

    - switch(true){

      case 조건 : 문장; break; default : 문장;}

- javascript 반복문

  - 반복 횟수를 명확하게 알면 for을 사용함
    - for(var count=초기값;조건;증감식){ 반복수행 문장; }
  - 특정 조건이 true 일때 계속 반복해야 하는 경우(조건에 따라 반복수행 여부 결정)
    - while(조건){반복 수행 문장;}
  - 최초 1번은 무조건 수행한 후에 조건에 따라 반복 수행 여부를 결정해야할 때
    - do while문을 사용함
      - do { 반복수행 문장;}while{조건};
  - 배열의 요소룰 or 객체의 속성을 순차적으로 꺼내올때 사용하는 반복문
    - for (var 변수 in 배열 or 객체){ 반복수행 문장;}

```javascript
//console.log(num); --- > 정상 실행
var num = 10; // --- > 선언 문장은 hoisting 되므로 밑에 있어도 사용 가능
//(자동으로 global.object인 window의 property로 추가됨. )

//템플릿 리터럴과 placeholer - 포맷형식 문자열에 실행시에 인수를 전달해서 출력하려면 
//`포맷형식 ${변수} 문자열` 

//자바스크립트의 형변환 - 값+"", String()  내장객체 제공(문자열로 변환)
// number(), window.parseInt(), window.parsefloat() - 정수나 실수로 변환
// !!값, Boolean() - 논리형으로 변환하려고 할 때 
```

- 자바 스크립트 객체 생성 방법
  - 객체 리터럴
    - JSON
      - 하나의 객체만 생성해서 사용하는 경우
  - 생성자 함수 정의
    - new 사용
      - 필요할 때마다 생성자함수로부터 객체 생성하는 경우
  - 프로퍼티
    - 객체에 포함된 데이터 하나를 가리켜서 객체의 프로퍼티라고 함
    - 프로퍼티의 이름 부분을 프로퍼티 이름 또는 키라고 부름
    - key를 유용하게 사용할 수 있음









