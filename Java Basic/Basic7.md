# 자바 기초 복습7

## First. package, import, 다형성, 인터페이스

- 시작 전 상속 추가정리
  - 단일 상속 - 클래스, extends
  - 다중 상속 - 인터페이스(속성+구현없는 기능 선언), implements
  - 포함관계 - has a 관계, A클래스와 B클래스의 관계는 멤버관계로 설계
  - 상속관계 - is a 관계
  - 상속제외되는 것 - private 속성, 메서드, 생성자메서드
- Package
  -  관계가 있는 인터페이스, 클래스, enum, 예외클래스들을 그룹핑 해 놓은것임.
  - Package 패키지명;으로 선언
  - 물리적으로 계층구조의 폴더로 생성
    - javac -d 패키지와클래스가 생성될 경로
    - java 패키지명.클래스명
    - 다른 package의 클래스를 사용할 경우 import를 해야함.
    - 자동으로 import 되는 패키지는 java.land.*;
- import
  - java.lang에 없는 소스코드를 사용하기 위해 로드 시키기 위한 것임.

- access modifier 정리

  |           | 외부패키지(상속x) | 외부패키지(상속) | 동일패키지 | 동일 클래스 |
  | :-------: | :---------------: | :--------------: | :--------: | :---------: |
  |  public   |         O         |        O         |     O      |      O      |
  | protected |         X         |        O         |     O      |      O      |
  | (default) |         X         |        X         |     O      |      O      |
  |  private  |         X         |        X         |     X      |      O      |

- 다형성 
  - 조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 하였음..!?
  - 부모클래스 객체 = new 자식클래스1();
               .....
               객체 = new 자식클래스2();
               .....
               객체 = new 자식클래스3();
    - 조상타입의 참조변수로 자손타입의 인스턴스를 참조할 수 있다.
    - 자손타입의 참조변수로 조상타입의 인스턴스를 참조할 수 없다
  - 다형성 객체는 access 가능한 속성은 부모에 선언된 속성만 access 가능
  - 다형성 객체가 호출 가능한 메서드는 부모에 선언된 메서드와 override된 자식클래스의 메서드
  - 다형성 객체에서 부모가 선언되지 않은 생성된 자식 객체의 속성이 메서드를 access하려면,
  - 선언된 부모 타입으로 형변환합니다.
- instanceof연산자
  - 왼쪽에는 참조변수를 오른쪽에는 타입(클래스명)이 피연산자로 위치하여 사용
    - boolean 값인 true와 false 중에 하나를 반환 
      - true를 얻으면 검사한 타입으로 형변환이 가능
    - 조상클래스의 경우에도 true를 얻음
- 추상클래스와 final
  - final
    - final은 멤버변수, 로컬변수, 메서드, 클래스 선언에서 쓰임
    - final 멤버변수는 상수이고 로컬변수도 상수이다.
    - public final 리턴타입 메서드명 ([매개변수 리스트]){...}는 override가 금지되고 확장도 금지
    - public final class 클래스이름 {}는 상속 불가
  - abstract 
    - 추상(선언만 존재하고 구현이 없음)
    - public abstract 리턴타입 메서드이름 ([매개변수 리스트]);
    - 클래스에 abstract를 선언하는 이유는 객체 생성을 못하는 것이며,
    - abstract메서드가 정의되어 있는 클래스는 abstract를 선언합니다.
- interface
  - 속성은 있으나 구현 없는 메서드 선언을 하기에 구현 메서드는 정의가 안됨 
    - 멤버변수 선언 불가
  - 그렇지만 신버전의 경우 함수적 프로그래밍을 위해 람다 표현식이 지원됨
    - 그래서 default로 선언된 구현 메서드 사용 가능
  - 함수는 변수 저장이 되며, 함수 내부에 함수를 정의할 수 있고 함수에서 함수를 리턴할 수 있다.
  - ex)  public final static int PACKAGE = 1; //선언가능,   public final static void method(){} //선언가능,  public abstract final void method2(){} //선언불가
  - public interface 인터페이스 이름 [extends 인터페이스]
  - 객체생성 불가, 참조변수의 타입으로는 선언가능, 인터페이스의 인스턴스를 생성하려면,
    - 반드시 객체 구현이 필요함

- 내부 클래스
  - member inner class
    -  protected , private 선언 가능
    - Inner class에서는 Enclosing class의 private 멤버를 객체 생성 없이 접근(읽기) 가능
    - Enclosing class에서 Inner class의 멤버를 접근(읽기)하려면 객체 생성해서 객체로 접근(읽기) 가능
  -  static Inner Class
    - Inner Class의 멤버속성 또는 멤버 메서드가 static으로 정의되어야할 경우,
    -  Inner Class가 static scope를 제공해야 하므로 static으로 선언해야 합니다.
  - local inner Class
    - Local Inner Class가 참조하는 local변수는 final이어야 합니다. 
    - Enclosing class에서 Local Inner Class 객체 생성 불가(메서드가 메모리에 올라와 있는 상태에서 객체를 생성해야 합니다.)