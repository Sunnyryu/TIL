# 자바 기초 복습8

## First. 유용한 클래스와 컬렉션  프레임웍

- 유용한 클래스
  - 깊은 복사 와 얕은 복사
    - 얕은 복사는 객체의 생성된 주소값을 할당하는 방식 유사함(동일한 객체를 참조) 
    - 깊은 복사는 객체의 모든 속성을 새로 생성해서 메모리에 새로운 동일한 객체를 생성 방식
    - 사용자 정의 클래스를 복제가능하도록 하려면 Cloneable을 구현함
  - notify(), notifyAll(), wait()는 멀티 스레드에서는 가능, 일반 메서드에서는 호출 불가, synchronized가 선언된 메서드에서 호출가능
  - java.lang.sString - 문자열 표현, 불변객체
    - String s = new String(new byte[]{65,66,67}); 
    - System.out.println(s); // System.out.println(s.toString())와 동일
    - A,B,C로 출력, 65,66,67을 ASCII 코드로 변환하여 출력됨.!
  - primitive date type을 문자열로 변환하려면 : String.valueOf() 또는 값+"(문자열)"을 함
  - split(구분자 or 정규표현식) - 토크나이징 해줌.. 문자열을 구분자로 쪼개어 문자열 배열로 리턴
  - join(결합문자, 문자열배열) - 문자열 배열의 요소를 하나씩 결합문자를 사용해서 하나의 문자열로 리턴함
  - 수학 계산에 유용한 메서드를 가지고 있는 클래스 java.land.Math라고 함.
  - 모두 객체로 구현해야 할경우, primitive data type을 객체로 wrapping 해야할 경우,
    boolean - > Boolean -> booleanValue()? - >( 문자열 "true")  Boolean.parseBoolean()
    byte - > Byte -> byteValue() - >(문자열 "100") Byte.parseByte()
    short - > Short -> shortValue() - >Short.parseShort() 
    char - > Character -> charValue() - >Character.parseCharacter() 
    int - > Integer - > intValue() - > Integer.parseInteger()
    long -> Long -> longValue() - > Long.parseLong()
    float - > Float -> floatValue() - >Float.parseFloat()
    double - > Double -> doubleValue() - > Double.parseDouble()
  - 정규표현식을 이용해서 data 처리해야 할 경우, 특정 패턴을 가지는 것을 추출하려고함.. - 특정 패턴을 객체로 생성
    - java.util.regex.Parttern 클래스의 compile("패턴")을 호출해야함 => Pattern 인스턴스 생성(new로 생성하는 것이 아님)
    - Matcher m = Parttern 인스턴스.matcher("처리할 대상 데이터") => Matcher 인스턴스 생성(new로 생성하는 것이 아님아님!!)
    - (실제 비교를 함~~~~) m.Matches() => true or false로 리턴(boolean으로 해줌)
  - 표준출력
    - 예전에는 java.io.InputStream을 사용함 
      - ex) InputStreamReader isr =new InputStreamReader(System.in);
            BufferReader br = new BufferReader(isr);
            br.readLine(); // enter 칠때까지 입력한 것을 넣는 것
    - String s = "월, 화, 수, 목, 금, 토, 일";
      - StringTokenizer sToken = new StringTokenizer(s, ",");
      - StringTokenizer는 내부에 포인터를 가지고 있고 구분자를 기준으로 
      - 포인터를 이동하면서  Token이 있으면 hasnextTokens() 메서드는 Token이 있으면,
      -  true를 리턴하고 없으면 false를 리턴한다.포인터가 가리키는 Token을 반환받으려면 ,
      - nextToken() 메서드를 사용하며, 이과정을 반복문에서 수행합니다
    
  - 컬렉션 프레윔웍
    
    - 컬렉션은 데이터 집합, 자료구조 같은 것임
    
    - 프레임워크는 표준화된 설계임
    
    - 컬렉션은 생성시에 저장될 요소의 크기를 설정하지 않아도 되고 동적으로 변경 가능!
    
      - list, set, Map 등이 쓰임
        - list는  순서가 있고 데이터 중복이 가능( 순서 보장!)
    
          - ArrayList(가벼워서 싱글쓰레드에서 사용), Vector(무거워서 멀티쓰레드에서 사용), LinkedList, Stack 등이 쓰이며 인덱스를 사용하여 접근
            - 인덱스(offset)로 저정된 요소
            - 저장할 떄에는 add(객체)나 add(index, 객체)
            - clear(), romeveAll() - 전부 다 삭제 할 때 
            - romove(객체), remove(index) - 특정한 것을 삭제할 때
            - size()
            - contains() 
            - get(index) 메서드를 사용하여 꺼내옴
            - iterater(꺼내올 때 사용함) - iterator()
    
        - set은 순서를 유지할 필요가 없는 것이 중복을 허용하지 않기 때문에.... index로 핸들링 하지 않음, iterator를 사용
    
        - Map은 순서는 유지 되지 않고 키는 중복 x, 값은 중복을 허용한다.(맵핑에 연관을 지으면 됩니다.)
          인덱스를 사용하지 않고 키를 사용하며 키는 중복과 널을 사용하지 않음 - 유니크 해야함
          
        - iterator<Book> - iterator()
          
          - while(iterator.hasNext()){}를 사용하여 True면 Book b = iterator.next()로 받음
          
        - Enumeration - hasMoreElement(), nextElement()를 사용함
    
          