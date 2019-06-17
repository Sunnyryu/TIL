# 자바 기초 복습3

## First. 반복문

- 반복문에서 많이 쓰이는 for, while, do while이 있습니다.
- 먼저 for에 대해서 예를 들어보자면,

```java
//위의 내용을 예를 통해 이해해보면,
public static void main(String[] args){
  	for(int i=1;i<=10;i++){ //for의 경우 옆의 코드처럼 i를 초기화 해주고 i<=10처럼
        //조건식을 만들어주고 i++를 처럼 증감식을 사용하는 방법으로 초기화를 합니다.
			if(i%2==1) System.out.println(i); 
		}
	for(int r=1;r<4;r++) {//옆의 코드는 이중 for문으로 for 안에 for를 더 넣어서 반복
        //을 하는 구조이다. 처음에 r이 1일때 안쪽 for문으로 들어가서 c=1 일 때부터 c가
        // 조건식을 넘기기 전까지 반복한 후에 끝나면 바깥 쪽 for문으로 나가는 코드이다.
        // 그래서 (1.1),(1.2),(1.3) 후에 c<4이므로 바깥쪽 for문으로 나간 후에
        // r=2로 반복하고 r<4일떄까지 반복한후에 r도 끝나면 마무리하는 반복문이다.
			for(int c=1;c<4;c++) {
				System.out.print("("+r+","+c+")"+"");
			}
			System.out.println();


    
    
    
    
  }


```

- 다음으로 while에 대해서 예를 들어보자면,

```java
public static void main(String[] args) {

		
		int count = 0;// while에서는 초기화를 while 밖에서 한 후에 
		int a = 0;// while문에 조건식을 작성합니다.
		while(count<10) {// 이떄는 count가 0부터 9까지 반복한 후에 마무리 되는 반복문
			a +=++count;
		}
		System.out.println("누적합" +a);

    int a = 0;
    Scanner scanner = new Scanner(System.in);
		System.out.print("입력해");
		while(true){// 이러한 반복문을 무한루프 식이라고 합니다.
			int 숫자 = scanner.nextInt(); 
			if(숫자==0) break; // 입력한 숫자가 0이면 종료가 되는 break를 넣어서 무한 
			if((숫자%3==1 || 숫자%3==2) && 숫자%5!=0) {// 루프가 끝낼 수 있게 
			  A++; // 되어있습니다.
			}
			
		}
		System.out.println("답:" +A);

}

```

- do while에 대해서도 예를 들어보자면,

```java
	public static void main(String[] args) {
		for(int i=1;i<=100;i++) {	
			System.out.printf("i=%d ", i);
		
			int tmp = i; // do while문의 경우에도 초기화는 밖에서 합니다.
			
			do { // do while문은 while문과 다르게 while문을 선 실행 후에
				if(tmp%10%3==0 && tmp%10!=0)//  조건을 체크하는 반복문 입니다.
					System.out.print("짝");
			} while ( (tmp= tmp / 10)!=0);
			
			System.out.println();
		}// 이 반복문을 끝나면 1부터 100까지 중에 3.6.9가 들어가는 것은 
	 	// 모두 짝이 나오게 되며, 99같은경우에는 짝짝으로 나오게 됩니다.
    }
```

