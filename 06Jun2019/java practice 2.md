#### Java 코딩 연습 2

##### 랜덤 제비 뽑기

```java
public static void main(String[] args) {
		int[] seat = new int[22]; 
		System.out.print("자리 배치는?");
		for(int i= 0;i <seat.length;i++) {
		seat[i] = (int)(Math.random()*23+1);
			for(int j = 0; j < i; j++) {
				if (seat[j] == seat[i]) {
					i--;
					break;
		
				}
			}
		} 
		String[] name = {"Sunny", "Ryu", "AD", "BK", "CU", "SD", "blank","cw","opa","TA","Just","isme","keny","ria","tvt","eils","sam","sung","emp","ssd","ubuntu","window","kingz"};
		System.out.println();
		for (int i = 0; i < seat.length; i++) {
			System.out.println(name[i]+":"+seat[i] +"\t");
			
		}
	}
```

