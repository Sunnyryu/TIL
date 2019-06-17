# 자바 기초 복습5

## First. 객체지향 프로그래밍 

- 객체지향언어
  
- 코드의 재사용을 높음.
  - 코드의 관리가 용이함.
  - 다양한 형태를 가질 수 있음
  - 신뢰성이 높은 프로그래밍이 가능함
  
- 클래스와 객체

  - 클래스
    - 속성(상태, data)과 기능(동작)으로 구성된 객체를 생성하기 위한 설계도
    - 구성요소는 클래스 선언, 멤버 필드(인스턴스 변수, 상수, 클래스변수),생성자 메서드(객체를 생성시 초기화를 수행), 멤버 메서드(기능 수행, 인스턴스 메서드, 클래스 메서드)
  - 객체
    - 현실 세계의 모든(유,무형) 것, 메모리에 생성되는 클래스의 인스턴스
      - 인스턴스는 클래스로부터 만들어진 객체임
  - 객체의 구성요소(속성과 기능)
    - 속성(멤버변수, 특성, 필드, 상태)
    - 기능(메서드,함수,행위)
      - ex) 속성 - 멤버변수 - int channel/ 기능 - 메서드 - channeulUp(){...}
  - 인스턴스의 생성
    - 클래스명 변수명; (ex) TV t; - 인스턴스가 생성되지 않아 참조변수로 아무것도 못함
    - 변수명 = new class명(); (ex) t  = new Tv(); - 인스턴스가 빈공간에 생성됨.
    - 메서드 :  특정 작업을 수행하는 일련의 문장들을 하나로 묶은 것임.
      - 수학의 함수와 유사함.
  - 클래스 구성요소 
    - 클래스 선언
      - **AccessModifier** [Modifier] **class** **이름** [extends 부모클래스]  [implements interface]{}
      - 클래스는 단일 상속, 인터페이스는 다중 상속 가능
      - AccessModifier - public , (default), Modifier - abstract, final
    - 멤버 필드
      - **AccessModifier** [Modifier] **타입 이름** [=초기값];
      - AccessModifier - public > protected > (default) > private
      - Modifier - final 선언 상수는 반드시 초기값 할당이 필요함, static은 동일한 클래스로부터 생성된 객체들간의 공유 변수, 1번만 메모리에 생성됨 (constant 영역, Method Area), 로컬변수는 매서드 안에서만 사용가능
      - 인스턴스 변수는 생성되는 객체마다 서로 다른 그 객체의 고유한 값을 가지는 변수임.
    - 생성자 메서드
      - **AccessModifier** 클래스이름([매개변수....]) {}
      - 클래스의 생성자 메서드는 1개 이상 선언 가능.
      - 생성자 메서드의 매개변수의 개수, 타입, 순서는 하나는 반드시 달라야함(overload 방지)
      - 클래스를 정의 시 생성자 메소드를 명시적으로 정의하지 않으면 JDK가 컴파일 시에 자동으로 default 생성자가 생성
      - 명시적 정의시 default 생성자가 자동으로 생성X
      - 생성자 메서드에서 클래스 내에 정의된 다른 생성자 호출 가능!
      - 생성자 메서드를 다른 생성자에서 호출 시, 이름으로 호출X this();으로 호출O
      - 다른 생성자에서 호출 시 첫째 라인에서 한번만 호출 가능!
    - 멤버 메서드
    - **AccessModifier** [Modifier] **리턴타입** **메서드이름** [매개변수 리스트]]  [throws 예외클래스..]{}
    - AccessModifier - public > protected > (default) > private
    - Modifier - abstract, final, static, synchronized, native
    - 리턴 타입 - void, primitive data type(8개), reference type(배열, enum, interface, class)
    - local 변수 - 메서드 내부에서 선언된 변수 [final] 타입 변수 = 초기값;
    - 메서드 내에 선언된 local 변수는 메모리에 메서드가 호출될 때 생성, 메서드 수행 이 종료시 Garbage collector가 제거하므로, local 변수는 메서드 외부에서는 참조가 안됨.
    - call by value : 메서드의 파라미터 타입이 primitive type이면 변수를 전달시 값을 복사하여 전달
    - call by referance : 메서드의 파라미터 타입이 reference data type이면 변수 전달시 변수의 주소값을 전달
    - 가변인자 파라미터는 메서드의 매개변수 순서상 가장 뒤에 오거나 단독으로 사용 가능
    - 로컬 변수는 사용전에 반드시 명시적 초기화가 필요하며, 로컬 변수는 final을 제외한 AccessModifier, Modifier는 선언 불가함.

  이제 예를 통해 위의 내용을 이해해보자면,

```java
//ex 1) 생성자 메서드에 관한 예제
public class Person {
	public String  id;
    private String name;
    //생성자 메서드를 명시적으로 정의하지 않으면 default 생성자를 컴파일시에 
    //JDK에 생성해줍니다.
}
//ex 2) 예제로 위의 개념 이해하기.
public class Student {//클래스 선언
//속성 선언	
private String studentId;
private int c;
private int linux;
private int java;

//객체 생성을 위한 초기화를 수행하는 생성자 메소드
public Student() { }
public Student(String studentId, int c, int linux, int java ) {
	this.studentId = studentId;
	this.c = c;
	this.linux = linux;
	this.java = java;
}

//기능을 수행하는 멤버 메서드
public String getStudentId() {
	return this.studentId;
}
public void setStudentId(String studentId) { 
	this.studentId = studentId;
}
public int getC() {
	return this.c;
}
public void setC(int c) {
	this.c = c;
}
public int getLinux() {
	return this.linux;
}
public void setLinux(int linux) {
	this.linux = linux;
}
public int getJava() {
	return this.java;
}
public void setJava(int java) {
	this.java = java;
}

public int getTotal() {
	return c+java+linux;
	//return getC()+getLinux()+getJava();
}

@Override
public String toString() {	
	return  "C: "+getC()+"점,"+" Linux: "+getLinux()+"점,"
              +" Java: "+getJava()+"점";
}



}//class end

public class StudentTest {

	public static void main(String[] args) {
		Student[] students = new Student[4];
		students[0] = new Student("SW05A01", 80, 90, 100);
		students[1] = new Student("SW05A02", 70, 80, 90);
		students[2] = new Student("SW05A03", 90, 90, 100);
		students[3] = new Student("SW05A04", 90, 90, 90);
		
		for(int i=0;i<students.length;i++) {
			System.out.println("=== "+students[i].getStudentId()+" 학생 점수 ====");
			System.out.println(students[i].toString());
			System.out.println("총점: "+students[i].getTotal()+"점");
			System.out.println("평균: "+students[i].getTotal()/3+"점");
		}
		
//		Student[] students2 = new Student[] {
//				new Student("SW05A01", 80, 90, 100),
//				new Student("SW05A02", 70, 80, 90),
//				new Student("SW05A03", 90, 90, 100),
//				new Student("SW05A04", 90, 90, 90)
//		};
		
//		 Student s1 =new Student("SW05A01", 80, 90, 100);
//		 System.out.println(s1);
//		System.out.print("C: "+s1.getC()+"점,");
//		System.out.print(" Linux: "+s1.getLinux()+"점,");
//		System.out.print(" Java: "+s1.getJava()+"점\n");
	

	}

}


```



