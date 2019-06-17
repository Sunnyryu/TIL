# 자바 기초 복습1

## First. Java란?

(1). Java는 객체 지향 언어이며, OS나 하드웨어에 영향을 받지 않음. (once write, Run anywhere)



Java는 Java application 과 JRE(Java Runtime Environment)로 이루어져 있음.

그리고  JRE에는 JVM(Java Virtual Machine )이 포함되어 있으며,

JVM이 OS에 명령을 내리고 OS가 Hardware에 명령을 내리는 구조라서,

OS가 다르더라도  영향을 받지 않음.



(2). Java는 대소문자를 구별함.



Java는 대소문자가 구별하지 않을 경우에 전혀 다른 것이 될 수 있기 때문에 주의해야함.



(3). Java는 Raw Data가 넘어오면 연산,조건, 반복 처리 후에 정보로 바꿔줌.



(4). Java는 컴파일과 인터프리터 언어로 이루어져 있음.



(5). Java는 네트워크, 분산 프로그래밍 구현 가능함. 



## Second. 변수와 상수란?



변수와 상수에 대해서 비교하자면, 

변수는 하나의 값을 저장하기 위한 공간이라면, 상수는 한번만 값을 저장할 수 있는 공간임.

변수는 a라는 값이 들어간 후에도 b라고 선언되면 바뀔 수 있지만 상수는 처음에 a라는 값이 설정되면 

바뀔 수 없다는 특성을 가짐.



변수는 primitive type과 reference type으로 구분되는데,



먼저 primitive type은 논리형, 수치형, 문자형으로 나눌 수 있음.



논리형은 boolean이 있으며, 참, 거짓으로 정의가 됌. (boolean은 형변환이 불가능함)

수치형(연산자와 함께 사용되어짐.)은 정수형인 byte, short, int, long이 있으며, 실수형은 float, double이 있으며, short는 2byte이고 int는 4byte, long은 8byte, float은 4byte, double은 8byte지만 실수형이 크기가 더 큼.

문자형은 문자 char이 있으며, 아스키 코드로 사용가능함.



그리고 형변환에 대해서 정의하자면, 크기가 작은 것에서 큰 것으로는 promotion이 되지만,

큰 것에서 작은 것(위의 설명처럼 long에서 float으로 바꿀때도 casting 해야함)이나 char와 byte, char와 short 같은 경우에는 Casting을 해줘야함.



타입선언을 할 때에는 

타입선언 변수; // 선언만 함.

타입선언 변수 = 값; // 선언 및 초기화를 함.



reference type은 class, interface, enum, 배열로 이뤄져 있으며, instance 화를 시키면,

reference 변수(객체).속성 = 값;  // 속성값 변경

reference 변수(객체).method(값); // 기능 호출



위의 설명을 예시로 들어보자면,



```java
public static void main(String[] args){
   int a = 1; // 변수 1로 초기화됨
   final int b = 2; // 상수 2로 초기화됨
   System.out.println(a); // a = 1으로 호출
   System.out.println(b); // b = 2으로 호출 
   int a = 3; // 3으로 다시 초기화 됌.
   //int b = 4; 상수의 경우에는 선언 후에 값이 변경 안됨.
   System.out.println(a); // a = 3으로 호출
  
   double c = 100;
   int score = (int)c; // double 타입의 변수 c를 int 타입으로 형변환 하기 위해 casting 함.
    
}
```



















 



