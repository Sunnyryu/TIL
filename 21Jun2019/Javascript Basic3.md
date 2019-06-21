## JavaScript

#### 복습



##### javascript





- 브라우저 객체 중 문서의 URL을 관리를 하기 위해 사용 - Location(location)
  
  - location.href
    - assign(url), relplace(url)
    - 현재 페이지 다시 보려면 reload
  
- 요청을 보낸 클라이언트의 브라우저 정보를 얻을 수 있는 객체 (Navigator)

  - html 문서에 포함된 클라이언트에 보내져서 클라이언트의 브라우저에서 실행되므로 자바 스크립트가 실행되는 브라우저 관련 정보
  - geolocation(위치정보를 사용할 수 있는 객체), appName(웹 브라우저 이름), onLine(네트워크 연결상태 확인하는 프로퍼티), platform(웹 브라우저가 실행중인 OS를 알려줌)

- 화면의 크기와 색상 정보를 관리 객체 - (Screen 객쳬)

  - 화면의 너비, 높이, orientation(가로인지 세로인지), colorDepth, pixelDepth

- 웹 페이지의 이력을 관리하는 객체 - history

  - length라는 필드에는 이동했던 것이 몇개 였는지 확인 가능
  - back() - 뒤로가는 메서드 forword() - 돌아오는 메서드, go(n|-n)

- 이벤트 처리

  - 이벤트 소스 객체.on이벤트 = function(){}// 이벤트 핸들러 함수
    - 하나의 이벤트에 대해서 하나의 핸들러만 등록 가능함
  - 이벤트소스객체.addEventListner("이벤트", 이벤트 핸들러 함수(함수 정의를 넣어줘도 되용);캡처링여부(default 값은 false));
  - 등록된 이벤트 제거
    - 이벤트소스객체.on이벤트 = null;
    - 이벤트소스객체.removeaddEventListner("이벤트", 이벤트 핸들러 함수)
    - 

- 브라우저에서 처리해주는 기본 이벤트 취소 :

  - 예) <a href=""></a>의 클릭 이벤트
  - 예) form 태그의 submit 이벤트(폼의 액션태그에 지정된 것에 데이터를 다 해줌) 
  - 방법 1: 이벤트소스객체.on이벤트 = function(){return false}
    - 이벤트 함수를 오버라이드 해서.
  - 방법 2: event.preventDefault()를 사용하여 취소함.

- 이벤트 전파 방식

  - 버블링
    - 대부분의 브라우저에서 기본으로 지원이 됨
    - 자식에서 부모로 이벤트가 전파됨..
      - 이벤트 버블링을 중단시키기 위해서는 event.stopPropagation()
  - 캡처링

- 웹 브라우저에서 문서의 내용을 표시하는 영역

  - 뷰포트라고 함(윈도우 좌표계라고 보면 되용)

  - 문서의 요소 객체는 박스모델이 적용되며 왼쪽 x좌표는 left속성, 왼쪽 상단의 y좌표는 top속성
  - 오른쪽 아래의 x좌표 right숙성, 오른쪽 아래의 Y좌표는 bottom속성
  - 너비는 width, 높이는 height 속성
    - 뷰포트의 너비 속성은 clientWidth, innerWidth
      - 스크롤 막대를 포함하는 것과 안포함하는 것으로 나눔
        - 포함하는 것이 innerWidth
    - 뷰포트의 높이 속성은 clientHeight, innerHeight
      - 스크롤 막대를 포함하는 것과 안포함하는 것으로 나눔
        - 포함하는 것이 innerHeight

- innerHTML , innerText

  - innerHTML 

    - 문서의 요소 객체.innerHTML = "<strong>강조체</strong>"

  - textContent 

    - 문서의 요소 객체.textcontent

  - innerText

    - 문서의 요소 객체.innerText는 강조하는 태그를 문자로 나오게 함.

    



