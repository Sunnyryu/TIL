#### Java 코딩 연습 1

##### x가 소수인지 아닌지 알아보기

```java
package practicemadecreativeperson5;

import java.util.Scanner;

public class primeNumber {

	public static void main(String[] args) {
		while(true) {
			System.out.print("숫자를 입력하세요(종료:0):");
			int num = getUserInput();
			if(num==0) {
				System.out.println("Bye~~");
				break; 
			} //0이면 반복문의 종료 조건을 만들어줌.
			
			int count = 0;
			for(int a=1;a<=num;a++) {
				while(num%a==0 ) {
					count++;
					break; 
						} // 8을 a로 나눴을 때 나머지가 0인것은 약수임.
					}
			if(count==2) {
				System.out.println(num+"소수입니다.");
            }// 자기를 나눴을 때 나머지가 0 인 것이 2개는 자기와 1밖에 없음. 
			else {
					System.out.println(num+"소수가 아닙니다.");
				// 1이나 소수가 아닌 것은 약수가 2개가 아님.
				} 	
				
			}			 
			
		}
	
	public static int getUserInput() {
		Scanner input = new Scanner(System.in);
		return input.nextInt();
	}

}


```

