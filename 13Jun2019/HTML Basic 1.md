## WEB

#### 웹

##### basic

```
webserver

browser - webserver

http protocol은 webserver 기본 포트가 80임.

어떤 page 요청이 없다면 웰컴 페이지로 해줌(ex) index, main 등)

응답으로 다운된 것을 해석(파싱)을 함 = > html을 계층 구조 = > 메모리에 객체 모델(트리구조)로 생성 / root = > branch => son

renderer (랜더링을 함) 
root  - head - tag
	 - body - tag
	 
랜더러가 객체마다 css를 검

리소스 위치나 라인타입, 서버정보, 브라우저 정보는 header에 보관되고
로그인정보 등은 Body에 포함됨(id,password 등)
응답할 때 필요한 정보 - header / 응답 시에 html 정보는 body에 저장
text 형태 (명령어, 내용 - text)
HTML - Link를 검(이미지도) - 같이 다운로드(client 쪽 응답으로 binery 보여줌)
server는 웹서버 기능만 있는 것이 있음
server는 webserver protocol 뿐만 아니라 webcontainer(jvm 들어있음 - application server) = was라고 함

netowrk 
	socket ( 전화와 비슷함 - 양방향 연결 - 계속 상태가 유지되어야함 ex) chatting)
	http는 비연결형 protocol (요청 보낼 때만 유지 시켜주면 됌)
요청 라인, 요청헤더, 공백라인, 메세지본문

상태라인이 중요 

100/Continue(나머지 정보 계속 요청)
200/OK(요청 완료)
400/Bad request(사용자의 잘못된 요청)
401/Unauthorized(인증이 필요한 페이지)
403/Forbidden(접근 금지)
404/not Found(요청한 페이지 없음 (url이 없음))
405/Method not allowed(허용되지 않은 http method 사용함)
500/internal server error(웹 서버 처리 x)

주소(도메인에서 address 받아옴)

형식 
get -  요청받은 URI의 정보를 검색하여 응답
post -  요청된 자원을 생성(CREATE)
put - 요청된 자원을 수정(UPDATE)한다. 내용 갱신을 위주
head -  GET방식과 동일하지만, 응답에 BODY가 없고 응답코드와 HEAD만 응답, 웹서버 정보확인, 헬스체크, 버젼확인, 최종 수정일자 확인등의 용도로 사용

get - 민감한 정보 보내면 url에 그대로 유출되기 때문에 post를 사용해서 보내야함...

웹 : 도메인/bbs/list.html (/는 root context임) 

```

##### 웹 역사

``` 
통신의 발달로 인해서 www가 나옴(1990년대 초반) - 팀 리버스가 만듬
 - 단순 html,view, 기본적으로 요청을 하고 응답이 올때까지 대기하는 동기 방식
 - 해석하고 랜더링이 되어야 쓸 수 있음 
 그리고 doc/test.html이 있어야만 다운 가능 (정적인 서비스) 
 
 동적으로 사용하기 위해 CGI(Common Gateway Interface)를 사용했음
 그런데 많은 인원이 접근하면 서버가 느려짐.. (못 버팀)
 그래서 단순 웹서버 기능만 있는 것이랑 요청을 별도 실행환경이 있는곳에서 실행함 (동적인 기능 실행 - 멀티 쓰레드 방식) - 여기서 back end로 분산기능을 추가하려고 했지만 (EJB) 실패함
 
 서버를 1개 두고 응답자를 여러개로 나누는 방식을 사용(MVC)
 (보완하기 위해 FRAMEWORK 사용!)
 
 "백엔드" 는 SERVLET(server applet) - JSD(model 방식) - EJB(분산처리) - JSP - Framework - 전자정보표준화

프로트엔드 
html (문서구조) - css(스타일) - Javascript(동작) - Rich client Internet, IE(Active X를 사용함)

IE가 다른 브라우저에서 호환이 안되는 문제가 있었음
W3C - 웹 표준화 하자고 함 
일정 Length가 안되면 막는 기능이 있어서 IE 단점이 있음

Ajax(javascript의 기능) -보통 일반사이트의 방식은 클라이언트가 요청하면 서버에서 클라이언트의 정보를 읽어들이고 요청한 정보의 페이지를 새로 만들어 보여주는 방식
	- 페이지의 전체 리로딩 없이 필요한 부분만을 바꿔서 보여주는 것이 가능

2007 ~ 2008년도에 등장한 Smart Phone으로 인해 웹에 영향을 받음
스마트폰 웹에서 멀티미디어 서비스를 이용하여 ACTIVE X를 이용하지 않아도 됌.
로컬 저장소를 확장시킴. 매번 HTML를 다운 받는게 아니라 Local에 다운 받은 후에 계속 사용가능 (오프라인 어플리케이션 캐시!), 
웹 소켓, 웹 통신 등이 이용 가능해짐

HTMP (HyperText Markup Language)
제2차 전자정보화표준화 (2010~2014)

서버와 독립적인 웹 어플리케이션이 가능해짐.
(Javascript에서 추가된 것이 많음)

HTML5의 등장으로 Javascript로 만들어진 게임이 가능해짐!

지도 기능, 웹소켓 기능도 허용됨. 
```

#### HTML

- HTML 태그
  - HTML에서 사용되는 명령어
  - 홑화살괄호로 표현함
  - 주석은 랜더링 되지 않음. 소스는 볼 수 있음.

```html
태그, 요소, 속성
태그와 요소
- HTML 페이지에서 객체를 만들 때 사용하는 것
- 시작 태그와 끝 태그의 사용법에 따른 구분
<a> Comment </a> 

속성
태그에 추가 정보를 부여할 때 사용
<t1 table = header></t1>

lang 속성
어떠한 언어로 만들어졌는지 확인 하는 것
ex) ko, en, ru

head 태그
body 태그에 필요한 스타일 시트와 Javascript를 제공하는 데 사용!!
ex? meta(추가정보 전달), title(제목), link(링크), style(스타일)
body 태그
사용자에게 실제로 보이는 부분

title 태그
html 태그의 lang 속성처럼 검색 엔진에게 웹 페이지의 제목과 관련된 정보를 주는 데 사용

title text 태그
제목 글자 태그는 제목을 입력할 때에 사용하는 태그
	
앵커 태그 
서로 다른 웹 페이지 사이 또는 웹 페이지 내부에서 특정한 위치로 이동할 때에 사용하는 태그
aref 사용

글자 형태 태그
글자에 형태와 의미를 부여할 때에 사용하는 태그
ex) h1 ~ h6

루비 문자
루비 문자는 문장 내의 임의의 문자에 대해 읽는 법을 알려주는 글자
ex) ruby(루비 문자 선언), rt(위에 위치하는 작은 문자 태그), rp(루비 사용시 출력x)

목록 태그
목록 태그는 목록을 생성할 때에 사용하는 태그, 웹 페이지의 내비게이션 메뉴를 생성할 때에 자주 사용

기본 목록
기본 목록을 생성할 때는 다음 태그를 사용

img
src 속성을 사용하여 이미지를 넣음
(해당 폴더에 없으면 경로도 다 넣어야함)
(width와 height로 크기 조절 가능)

audio
src, control, autoplay, loop 등을 사용하여 만듭니다.

video
width, height, autoplay, controls, loop 등을 사용하여 만든다.

다른 링크로 연결 할 때
target을 이용하여 합니다.

테이블 삽입
table(표를 넣고자 함), tr 하나의 행, th 테이블의 제목, td 열 제목에 나타나는 첫 번째 행의 셀 제외한 각각의 값
```













