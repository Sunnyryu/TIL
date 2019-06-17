## HTML+CSS

#### Basic

HTML과 CSS

HTML

```html
<!DOCTYPE html> <!-- !은 타입선언-->
<html> <!-- Tag는 내용에 대해서 적용할 구조에 관련된 명령어 역할을 함, 파서가 해석을 함-->
    <!-- 파서가 생성해주는 결과물은 Dom(Document object model) tree를 생성함)-->
    <!-- DOM tree 파서 밑에 html 밑에 Head와 body로 트리구조로 이어짐..-->
  <head>
      <!-- 폰트 등은 Randerer가 적용시켜줌-->
<!-- ex) 외부에서 가져올 때 사용하는 것link href="1.css" rel="stylesheet" type="text/css"(html과 같은 위치에 저장되어 있어야함-->
    </head>  
    
</html>
```

- HTML4/XHTML에서는 <div>를 이용해서 header, menu, content, side, footer 영역을 만들었었음. 
- HTML5는 <header>, <nav>,<aside>,<footer>,<section>,<article> 등으로 나눔.
- DTD나 schema 문서대로 잘 작성하는 대로 validator로 검사를 하면 Wellformed 하다고 함.(1차적 검사)

CSS

```
html에서는 style 태그를 하는 역할임
<style> 태그 내 h3
CSS 선택자
color: rod; (css 명령/색을 red로 변경)
text-shadow : 글자에 그림자를 넣음(2px 2px 10px gray)
<p> : 단락을 정의하는 문단요소로서 한 문단을 나타냄

<span> :특정 부분 글자를 CSS로 꾸미기 위해 영역 지정(너비,폭을 분리..)
<div> : division의 줄임말로 분할하라는 뜻이며, 박스라고 생각하면 편함(콘텐츠를 담는 것)
div에서는 class와 id를 쓰는데
class는 여러 태그에 중복 사용이 가능하며, .class로 나타냄
id는 중복사용이 불가능하며, 다중의 id 부여x, #id로 나타냄
list-style-type: 각 항목에 붙는 글머리 형태 지정
주석 : /* */
- text-shadow; = textshadow
- 같은 태그라도 id속성이나 name이나 class 속성으로 구별하여 따로 구분하여 설정할 수 있음
```



```
CSS 선택자 : css를 적용하고자 하는 영역 
태그 선택자 : 태그의 영역 선택하고 이후에 오는 CSS 명령을 해당 영역에 적용(p) => (선택자에 태그명 사용)
id선택자(중복사용이 불가능하며, 다중의 id 부여x, #id로 나타냄)
ex) id = 'p1'
#p1 => id = 'p1' 영역선택
class선택자(여러태그에 중복사용 가능 두 군데 이상의 특정 영역 지정하여 동일한 CSS 적용,클래스명 앞에 점(.) 붙임
)
ex) <li><span class = 'green'>루비</span>
body: <body> 태그 영역에 들어가는 값을 선택
p: p 태그 영역 선택
```



```
박스 모델: 박스 형태로 된 모든 html 요소
경계선(border), 마진(margin), 패딩(padding) 지정 가능
border : 경계선을 그리는 데 사용되는 속성
	solid(실선),double(이중실선),dotted(점선),dashed(줄선)
padding : 경계선 내부 간격
	글자와 경계선 사이의 간격(padding/padding-top.right.bottom.left)
width /height 사용 (박스의 너비, 높이)
margin : 경계선 외부 간격
	(margin-top 등을 사용 단위는 보통 px)
별도 설정이 없어도 HTML 요소는 기본적인 PADDING/MARGIN 가짐
(*{padding: 0; margin: 0;} - 전체 선택자에 의해 선택된 모든 요소에서 패딩과 마진을 0으로 초기화)
```



```
ex) background-color: blue; (파란색으로 배경 설정)
<div> 박스 형태 요소 만들기 / #button id=‘button’의 영역을 선택
background-image: url(‘img/bg.jpg’); - 배경 이미지 삽입에 사용
,url 뒤 괄호 안에 경로 포함한 배경 이미지 파일 이름 입력
background-repeat - 웹 브라우저 화면보다 배경 이미지가 작을 경우 배경 이미지가 반복
background-repeat: no-repeat; (no-repeat 속성값)
```



```
ex) border: solid 1px #000000; (실선 / 1px /000000색)
    border-collapse: collapse; 테이블 경계선을 하나의 가는 실선으로 그림
생략할 경우 이중실선(border-collapse: collapse;는 서로 이웃하는 테이블이나 셀의 테두리선을 겹쳐서 표현하게 됌)
text-align: center : text-align 속성, center 속성값으로 테이블 셀 안 요소를 중앙정렬
```

```
- 레이아웃 : 웹 페이지에 박스, 텍스트, 이미지 등 HTML 요소 배치하는 것
	(수평방향은 인라인/ 수직방향은 블록)
	인라인(붉은색 표시 이미지, 텍스트 : 가로 방향으로 배치되는 HTML 요소)
	(img, span 태그 등)
	블록 요소(파란색 표시 박스 : 세로 방향으로 배치되는 HTML 요소)
	(<p>, <div> 태그 등)
  display 속성(기본속성 무시, 인라인 블록 사용)
  v_menu li / #h_menu li (후손 선택자 - 선택자 아래 다시 선택자 설정)
display: inline; <li> 태그가 기본으로 가지는 블록을 인라인으로 변경
float : 요소를 왼쪽 또는 오른쪽에 배치
clear 속성 :float 속성 사용된 요소가 그 뒤 오는 요소와 겹쳐 화면 깨지는 경우 뒤 요소의 float 속성 해제하여 새로운 줄에 배치
clear: both; (앞의 float: left; 와 float: right; 에서 사용된 float 속성 해제)



```



```css
@charset "utf-8";
/* CSS document */
p{} /* 태그 선택자*/
# header /* id 선택자 예 */
. class속성값 {......} /* class 선택자 넣을 때*/
/*div p span, id 기본구조, class 구조등도 사용
<div id="header">
<div id="side">
<div id= "form">
<div id= "row">
*/
```

```
추가설명 
* = html 모든 태그
기본 속성 선택자는 특정한 속성의 존재 유무와 속성 값을 판별할 때에 사용함
문자열 속성 선택자는 태그가 가지고 있는 속성의 특정한 문자열을 확인함
- 후손 선택자는 특정한 태그 아래에 있는 후손을 선택할 때 사용하는 선택자
- 자손 선택자는 특정한 태그 아래에 있는 자손을 선택할 때 사용하는 선택자
- 동위 선택자는 동위 관계에서 뒤에 위치한 태그를 선택할 때 사용하는 선택자
- 반응 선택자는 사용자의 반응으로 생성되는 특정한 상태를 선택하는 선택자
-상태 선택자는 입력 양식의 상태를 선택할 때 사용하는 선택자
일반 구조 선택자는 특정한 위치에 있는 태그를 선택하는 선택자(자손 선택자와 많이 병행해서 사용)
-형태 구조 선택자는 일반 구조 선택자와 비슷하지만 태그 형태를 구분
-문자 선택자는 태그 내부의 특정한 조건의 문자를 선택하는 선택자
-반응 문자 선택자는 사용자가 문자와 반응해서 생기는 영역을 선택하는 선택자
-링크 선택자는 href 속성을 가지고 있는 a 태그와 한 번 이상 다녀온 링크를 선택할 수 있는 선택자
부정 선택자는 지금까지 배운 선택자를 모두 반대로 적용할 수 있게 만드는 선택자
```



```
-CSS에서 사용하는 크기 단위는 %, em, cm, mm, inch, px임
-display 속성(태그의 영역 표현 방식을 지정하는 속성)
(none,block,inline,inline-block 사용)
-visibility 속성(대상을 보이거나 보이지 않게 지정하는 속성)
(visible(태그를 보이게 만듬), hidden(태그를 안보이게 만듬), collapse(테이블 태그 안보이게 만듬))
-opacity 속성(대상의 투명도 지정(0~1 사용))

-박스속성(웹 페이지의 레이아웃을 구성할 때 가장 중요한 속성)
 -width 속성과 height 속성, margin 속성과 padding 속성,border 속성을 합쳐서 박스속성이라고 함

```



```
-position 속성
태그의 위치 설정 방법을 변경할 때 사용
	static(위에서 아래로),relative(초기 상태에서 상하좌우),absolute(절대위치 좌표를 설정,fixed 사용(화면을 기준으로 절대 위치 좌표 설정)
	position 속성은 스타일 속성과 사용(must)
	z-index 속성(HTML 태그는 아래 입력한 태그가 위로 올라오며, 큰 값일 수록 위로 올라옴)
-overflow 속성
(내부의 요소가 부모의 범위를 벗어날 때 어떻게 처리할지 지정하는 속성)
(hidden과 scroll 사용 - 영역을 벗어나는 것을 보이지 않게 하거나 벗어나는 부분을 스크롤로 만듬)
-float 속성
웹 페이지 레이아웃을 구성할 때에 반드시 사용하는 속성(부유하는 대상을 만들 때에 사용하는 속성) = > left와 right 사용 (태그를 왼쪽/오른쪽으로 붙임)

- text-shadow 속성
글자에 그림자를 부여하는 속성/text-shadow:5px 5px 5px red(오른쪽/ 아래 / 흐림도 / 색)
- box-shadow 속성
박스에 그림자를 부여하는 속성/box-shadow:5px 5px 5px blue(오른쪽/ 아래/ 흐림도/ 색)

- 벤더 프리픽스 
벤더 프리픽스는 웹 브라우저 공급 업체에서 제공하는 실험적인 기능을 사용할 때 사용(구글, IE, 모질라 등)

- 그레디언트
2가지 이상의 색상을 혼합한 색을 만들어 채색하는 기능
linear-gradient() 함수(선형 그레이디언트를 만들 때에 사용)
```



