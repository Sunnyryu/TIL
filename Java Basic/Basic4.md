# 자바 기초 복습4

## First. 배열

- 배열의 정의 
  - 배열은 같은 타입의 여러 변수를 하나의 묶음으로 만든 것임.

- 배열의 생성
  - 타입[] = 변수이름;
  - 변수이름 = new 타입[길이];
- 배열의 길이와 index
  - 인덱스는 배열의 요소마다 붙어진 일련번호라고 생각하면 되며, 배열의 각 저장공간을 배열의 요소라고 함.
  - 배열의 길이는 int 범위의 0과 양의 정수여야 함!!
- String 배열
  - String[] name = new String[3]; // 3개의 문자열을 담을 수 잇는 배열 생성
  - Stringclass는 char 배열에 메서드를 추가한 것이라고 생각하면 됨.

- 다차원 배열
  - 2차원 배열
    - 선언하는 방법은 크게 3가지가 있는데,  타입[][] 변수이름;, 타입 변수이름[][];, 타입[] 변수이름[];

예를 통해서 이해해보자면,

```java
//ex 1)
	public static void main(String[] args) {
		int[] score = new int[5]; // 선언만 함(묵시적) - MainThread가 할당을 받음. 객체 취급함 - score는 reference 주소값이 저장됨
		//System.out.println(score); - null이라 출력됨, 로컬변수는 초기화 시키지 않고 사용해서 오류가 발생함
	  // heap이라는 메모리에 자신이 들어갈 수 있는 공간이 있으면 들어감. 20byte를 할당함 - int가 4byte고 5개 이므로 
		// 0x100 0x200 0x300 등으로 저장!? 선언안하면 기본값 0으로 저장
		System.out.println("score배열의 요소 개수:"+ score.length); //5
		
		for(int i=0;i<score.length;i++) {
			System.out.println("Score["+i+"]="+score[i]);
		} // Score[0] = 0, Score[1] = 0, Score[2] = 0, Score[3] = 0, 
          // Score[4] = 0
		//배열 선언, 생성, 명시적 초기화 
		int[] score2 = new int[] {100, 300, 500, 700, 900, 901, 902};
		System.out.println("score2배열의 요소 개수:"+ score2.length);//7
		for(int num : score2) {
			System.out.println(num);
		}// 100, 300, 500, 700, 900, 901, 902(한줄씩 띄어서 나옴)
	
	
		int[] score3 = {100,300,500,700};
		System.out.println("score3배열의 요소 개수 :" + score3.length);//4
		for (int num : score3) {
			System.out.println(num);// 100, 300, 500, 700(한줄씩 띄어서 출력)
		}
	
	}

//ex2 )
	public static void main(String[] args) {
		int[] lotto = new int[6]; // 로또 번호 지정을 배열방 준비
		//1~45 범위에서 난수 생성에서 배열의 첫번째 방에 저장
		//1~45 범위에서 난수 생성에서 배열의 두번째 방에 저장(중복금지!)
		//다를 경우에만 두번째 방에 지정
		//중복되지 않는 로또 번호 출력
		System.out.print("로또 번호 맞춰보자");
		for(int i= 0;i <lotto.length;i++) {
		lotto[i] = (int)(Math.random()*45+1);
			for(int j = 0; j < i; j++) {
				if (lotto[j] == lotto[i]) {
					i--;
					break; // 같은 경우 if문을 빠져나옴.
		
				}
			}
		}
		
		for (int i = 0; i < lotto.length; i++) {
			System.out.print(lotto[i] + "      ");
		}// 결과 값이 임의 6개가 나오게 됨.
	}
//ex 3)
	public static void main(String[] args) {
		int[][] nums;// 배열 선언
		int nums2[][];
		int[] nums3[];
		nums = new int[5][5]; //배열생성
		nums2 = new int[5][];
		//nums3 = new int[][5];
		nums3 = new int[][] {{1, 2, 3}, 
			{4, 5, 6, 7}, {8, 9, 10, 11, 12}}; // 배열의 요소 초기화
		System.out.println(nums3.length);// 2차원 구조의 행 개수, 1차원 배열의 총 개수 (3)
		System.out.println(nums3[0].length);// 첫번째 1차원 배열의 요소 개수 (3)
		System.out.println(nums3[1].length);// 두번째 1차원 배열의 요소의 개수 (4)
		System.out.println(nums3[2].length);// 세번째 1차원 배열의 요소 개수 (5)
		
		for(int r=0;r<nums3.length;r++) {
			for(int c=0;c<nums3[r].length;c++) {
				System.out.print(nums3[r][c]+" ");
			}							//1 2 3
			System.out.println();		//4 5 6 7
		} 								//8 9 10 11 12
 }	
// ex 4)
	public static void main(String[] args) {
		int[][] array1 = new int[3][3];
		
		for(int r=0;r<array1.length;r++) {
			for(int c=0;c<array1[r].length;c++) {
				array1[r][c] = (int)(Math.random()*100+1);//1~100까지의 난수 생성
				
				
			}
		}
		System.out.println("첫번째배열");
		for(int r=0;r<array1.length;r++) {
			for(int c=0;c<array1[r].length;c++) {
				System.out.printf("%3d", array1[r][c]);
				
			}
			System.out.println();
			
		}
		
		int sum =0, count=0, min = 100 , max=0;
		 for(int r=0;r<array1.length;r++) {
			 for(int c=0;c<array1[r].length;c++) {
				 sum+=array1[r][c] ;
				 if(min>array1[r][c]) min = array1[r][c]; // 최소값
				 if(max<array1[r][c]) max = array1[r][c]; // 최대값
			 }
			 count+=array1[r].length;
			 System.out.println();
		 
		 }
		 
		 System.out.println("배열의 모든 요소의 합 :" +sum);
		 System.out.println("배열의 모든 요소의 평균 :" +Math.round(sum*100.0/count)/100.0);
		 System.out.println("배열의 모든 요소의 최소값:" +min);
		 System.out.println("배열의 모든 요소의 최대값 :" +max);		
			
		
		
		

	}


```

- 배열은 Reference Type, 객체로 취급하며, new 키워드로 생성함.
  new 키워드로 생성할 경우 heap메모리에 생성되며, 배열은 타입에 따라서 요소(element)값을  기본값으로 저장하며, 배열은 객체로 생성되면 자동으로 length 속성(멤버필드)에 요소 개수 size가 저장됩니다.