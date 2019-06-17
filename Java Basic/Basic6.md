# 자바 기초 복습6

## First. 객체지향 프로그래밍 2

- 상속
  
- 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것임
  - 클래스 상속은 단일 상속
  -  명시적 부모 클래스 선언 없으면 java.lang.Object 최상위 클래스를 자동 상속받음
  -  부모의 속성과 메서드를 상속받습니다. - private 선언 속성과 메서드 상속 안됨, 생성자 메서드 상속 안됨. (멤버만 상속가능)
  - 단일 상속은 extends
  - 자식 클래스의 모든 생성자의 첫번째 줄에서 명시적 생성자 호출이 없는 경우,
    - 부모 클래스의 default 생성자를 호출하는 super()가 자동으로 컴파일시에 포함됨.
  - 자손 클래의 맴버 개수가 조상 클래스보다 많거나 같음.
  
  예를 들어 이해해보자면,

```java
// ex 1)
package lab.java.core;

class Parent {
    String name = "parent";
    private int money =1000000000;
    public void work() {
    	System.out.println("IT");
    }
    private void hobby() {
    	System.out.println("2Job");
    }
}

class Child extends Parent{ //extends를 통해 Parent를 상속받는다는 걸 알 수 있음.
	
}

public class ExtendsTest1 {
	public static void main(String[] args) {
		Child c1 = new Child();
		System.out.println(c1.name);
		c1.name = "child";
		System.out.println(c1.name);
		c1.work();		
	}
}


```

- override (오버라이딩)
  - 상속받은 메서드를 그대로 사용하는 것이 아니라, 메서드 선언은 동일하게 선언하고, 메서드의 내용을 개선하는 것임.
  - 조건
    - AccessModifier가 동일하거나 Scope이 넓어야함
    - 리턴 타입은 반드시 동일 해야함
    - 메서드의 이름은 반드시 동일해야함
    - 메서드의 매겨변수 순서, 개수, 타입 모두 동일 해야함.
    - throw 예외클래스는 생략하거나, 동일하게 선언하거나 하위 예외 클래스 선언 가능!
    - 자식클래스에서는 부모로부터 상속받은 메서드를 overload와 override 가능함.
    - override 메서드는 한개만 재정의 가능하며, overload는 개수 제한 없이 가능합니다.
    - AccessModifier는 public, protected (default) private가 쓰임
    - modifier는 final, static, abstract가 사용됨.
- overloading 
  - 기존에 없는 새로운 메서드를 정의하는 것(new)
- Super
  - 자손 클래스에서 조상 클래스로 부터 상속받은 멤버를 참조하는 사용되는 참조변수임.
  - super()로도 사용됨.
  - 조상 클래스의 생성자를 호출되는 사용됨.

예를 통해 이해해보자면,

```java
//ex 1) super를 사용한 예제
class Parent2 {
   public Parent2() {
	   System.out.println(1);   
 	   }
   public Parent2(String talent) {
	   System.out.println(2);
   }
}

class Child2 extends Parent2{ //상속
	public Child2() {
		super("IT"); //super()
		System.out.println(3);
	}
	public Child2(String talent) {		
		 System.out.println(4);
	}
}

public class ExtendsTest2 {
	public static void main(String[] args) {
		 Child2 c2 = new Child2();
		 Child2 c3 = new Child2("DB");
	}
}
ex 2) 오버로딩과 오버라이딩의 예시
class Parent5 {   
	protected  int add(int a, int b) throws IOException{
		return a+b;
	}
}

class Child5 extends Parent5{ //상속	 
	void  add(int a, int b, int c) {//overload한 메서드
		 System.out.println((a+b)*0.9);
	}
	protected int add(int a, int b) {//override메서드
		return (int)((a+b)*0.9);
	}
}


public class ExtendsTest5 {
	public static void main(String[] args) {
		  Child5 c5 = new Child5();
		  System.out.println(c5.add(3,  4));
	}
}


```



