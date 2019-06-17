#### Java 코딩 연습 3

##### 야구 게임 만들기

```java
package practicemadecreativeperson;

public class BaseBall {
public static int player = 0;
public static int outCount = 0;
public static int strike = 0;
public static int ball = 0;

public static void getStatus() {
	System.out.println(outCount+" 아웃  "+ball+" 볼  "+strike+" 스트라이크 "); 
}
public static boolean isStrike() {
	double a = (int)(Math.random()*2);
		if(a==0) {
			return true;
		}
		else{
			return false;
		}
}
}
public class BaseBallTest {

	public static void main(String[] args) {
		BaseBall b = new BaseBall();

	for(;;) {
		if(b.outCount==1 || b.outCount==2) {
			System.out.println("다음타자");
		}
		else if(b.outCount==3) {
			System.out.println("이닝종료");
			System.exit(0);
		}
		
		
		
		System.out.println("*****"+ ++b.player+"번째 선수 타석*****");
			for(;;){
				if(b.isStrike()) {
					System.out.println("투수 와인드업 => 볼!!");
					++b.ball;	
				}else {
					System.out.println("투수 와인드업=> 스트라이크!!");
					++b.strike;
		}

		b.getStatus();
		if(b.ball==4) {
			b.strike = 0;
			b.ball = 0;
			System.out.println("볼넷");
			System.out.println("다음타자");
			++b.player;
			System.out.println("*****"+ b.player+"번째 선수 타석*****");
		}
		else if(b.strike==3) {
			System.out.println("\n 삼진"+" "+ ++b.outCount+"아웃");
			b.strike = 0;
			b.ball = 0;
			break;
		
		}
	
		}
	
	}

	}
}
```

