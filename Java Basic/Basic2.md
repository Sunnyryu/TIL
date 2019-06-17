# 자바 기초 복습2

## First. 연산자

- 연산자란, 연산을 수행하는 것이라고 생각합니다.(ex. +,-,*,/ 등)

- 연산자를 사용되는 대상을 피연산자라고 하며, 변수, 상수, 리터럴, 수식 등이 있습니다.

연산자에 대한 종류를 나누자면, 크게 단항연산자, 이항연산자, 삼항연산자로 나뉩니다.

- 단항연산자는 +, -(sign 연산자), ++(1씩 증가), --(1씩 감소), 보수 등이 있습니다.

- 이항연산자는 산술연산자와 비교연산자와 비교, 비트, 논리, shift연산자로 나뉩니다.
  -  *, /, +, -, % 등 사칙연산과 나머지의 기호를 산술연산자라고 합니다.
  - ,>=,<=,<,==,!= 등 값을 비교하는 기호를 비교연산자라고 합니다.
  -  &&, ||, !, &, ^, ~ 등 AND와 OR 등 조건으로 연결되는 것을 논리연산자라고 합니다.
  - <<, >>, >>. 등 2진수의 자릿수를 이동시키는 것을 shift 연산자라고 합니다.
- 삼항연산자는 ?와 대입연산자로 나뉩니다.

```java
//위의 내용을 예를 통해 이해해보면,
public static void main(String[] args){
    int a = 10, int b = 20; // 변수 a를 10, b를 2으로 정의했을 때
    System.out.println((b%a)); // 20을 10으로 나눴을 때 나머지가 0이므로 0이 호출됨
    System.out.println((b*a)); // 20을 10으로 곱했을 때는 200이므로 200이 호출됨
    System.out.println((b^a)); // 20과 10을 2진법으로 바꿔서 해야하며, 
    						   // ^는 둘이 같지 않으면 1이기 떄문에 30이 호출됨
    System.out.println((b|a)); // |는 1과 0이 만났을 때 하나라도 1이면 1이기에 30이 								   // 호출됨
    System.out.println((b&a)); // &는 2진법으로 바꿔서 1과 1이 만나지 않으면 
    						   // 0이기 떄문에. 10100과 1010을 더하면 0이 나옵니다.
    System.out.println(a+b>25?"크다":"작다"); // ?는 앞의 말이 맞으면 뒤의 a:b에서 a	// 를 호출하며, 틀리면 b를 호출하는데 a+b= 30이므로 30>25라 참이기에 크다로 호출됨.
}

```

## Second. 조건문(if, else if, else)

#### if, else if, else

- if에 앞서 조건문을 예로 들어 설명해보면 if(5>4)가 맞으면 참, 틀리면 거짓이라고 했을 때 5는 4보다 크므로 참이 된다. 이러한 식을 조건문이라고 하는데, 조건문에 쓰이는 if, else if, else를 예제를 통해 이해해보자면, 

```java
#ex) 한 음식점에서 감자치킨, 양파피자, 베이컨샐러드를 파는데, 이것을 먹은 후에 평점을 준다고 했을 때, 식을 만들어서 설명해보겠습니다. 

   public class food 
   	public static void main(String[] args) {
   	 	System.out.println("감자치킨의 평점을 적어주세요.:");
			int 감자치킨 = scanner.nextInt();
		System.out.println("양파피자의 평점을 적어주세요.:");
			int 양파피자 = scanner.nextInt();
		System.out.println("베이컨샐러드의 평점을 적어주세요.:");
			int 베이컨샐러드 = scanner.nextInt();
		System.out.println("평가를 해주시는 음식의 개수는?");
		int 개수 = scanner.nextInt();
		int 총평점 = 감자치킨 + 양파피자 + 베이컨샐러드;
		int 평균 = 총합/개수;
		System.out.println("총평점과 평균은?" + 총평점 + ".." + 평균);
		
		int A = 감자치킨, B = 양파피자, C = 베이컨샐러드;
       
       if(A>B && B>C) {
			System.out.println("감자치킨이 가장 맛있고 베이컨 샐러드가 별로구나.");
		} else if(A>C && C>B) {
			System.out.println("감자치킨이 가장 맛있고 양파피자가 별로구나.");
		} else if(B>C && C>A) {
			System.out.println("양파피자가 가장 맛있고 감자치킨이 별로구나.");
		} else if(B>A && B>C) {
			System.out.println("양파피자가 가장 맛있고 베이컨 샐러드가 별로구나.");
		} else if(C>B && B>A) {
			System.out.println("베이컨 샐러드가 가장 맛있고 감자치킨이 별로구나.");
		} else if(C>A && C>B) {
			System.out.println("베이컨 샐러드가 가장 맛있고 양파피자가 별로구나.");	
		} 
		else {
			System.out.println("맛이 비슷한 것이 있어 정확한 평가는 못하겠어.");
		}
	}
}
// 위의 문제에서 if와 else와 else if에 대해서 설명해보자면
// if는 하나의 조건문이고 else if는 if와는 다른 조건을 가진 조건문이며, else는 if와 else if가 모두 아닌 조건일 때에 쓰이는 것이다. 보통 if와 else나 if와 else, else if가 모두 쓰이는 조건문등이 있다. 위의 문제 같이 조건문을 활용하면 비교도 할 수 있음.
    
```





