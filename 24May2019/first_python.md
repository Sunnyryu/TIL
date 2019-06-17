# Python( Watching PY4E Youtube)



### 1. Basic

#### hi Python!(안녕 파이썬!)

##### before start!

파이썬을 배우기 전에 컴퓨터 내부 구조에 대해서 배웠습니다.

CPU // 입력장치 // 출력장치 // 메인 메모리 // 보조기억장치에 대해 간단히 정리하자면,,

CPU (Central Processing Unit) : 프로그램 실행 , alway question for what the next?, 처리능력 우수

입력장치  : 사람의 의해.. 정보 입력 받는 기기 (우리가 즐겨 사용하는 키보드, 마우스, 터치 스크린 등)

출력장치 : 처리된 정보의 결과를 보여주는 기계.. (스피커, 프린터 , DVD 기록기 등)

메인 메모리 : 적은 양의 정보를 저장하는 장치, 속도는 굿, 컴퓨터 종료시 알콜 같이 사라지는 메모리..

보조 기억장치 : 지우지 않는 이상.. 정보를 계속 보존! (SDD, HDD 등)

##### What`s the Python?

- 귀도 반 로섬이라는 분이 만든 것!

- Month Python`s Flying에서 이름을 따온 것!

- 문법 에러가 뜬다는 것은 사랑 표현을 잘 못하는 것!

- cmd를 이용하거나 에디터를 이용해서 편하게 배울 수 있는 언어인 것!

  ```python
  x=1
  print(x)
  1
  x = x + 1
  print(x)
  2
  exit()
  # 간단한 파이썬의 예.. 
  ```

  

##### start Python!

- 예약어와 문장 이용 하기! (예를 들어 설명하기)

  - 예약어 

    예약어는 쉽게 생각해서 파이썬이 정한 의미로만 쓰이는 특별한 단어인 것.

    ex) and del global not with as elif if or yield assert else import pass
    break except in raise class finally is return continue for lambda try
    def from nonlocal while

    (이와 같이 예약어는 많다..)

  - 순차문

  ```python
  x = 2
  print(x) # 2를 출력
  x = x + 3
  print(x) # 5를 출력
  
  ```

  - 조건문 

  ```python
  x = 4
  if x < 10:
  	print('Smaller')# Smaller가 출력
  if x > 15:
      print('Bigger') # bigger가 출력
  print('finish') # finish가 출력  
  ```

  - 반복문

  ```python
  n = 6
  while n > 0:
    print(n) # 6,5,4,3,2,1을 출력합니다.
    n = n - 1
  print('Blastoff!') # Blastoff를 출력합니다.
  ```

- Print Hello Sunny!

  ```python
  print("Hello Sunny")
  ```

 ##### Varialbles, Expressions, and Statements!

- constants(상수)

  - 상수는 값이 변하지 않음.

  ```python
  print(100) # 100을 출력 - 100이 상수
  print(22.2) # 22.2를 출력 - 22.2가 상수
  print('Hello Sunny') # Hello Sunny를 출력 Hello Sunny가 상수
  ```

- Variables(변수)

  - 변수를 통해 메모리를 할당하고 이름을 지어  원하는 데이터를 넣을 수 있음

  ```python
  x = 10.0
  print(x)  # 10.0이 출력
  y = 15.5
  print(y) # 15.5가 출력
  x = 2222
  print(x) # 2222가 출력됨. 위의 상수와 다르게 x값을 선언하면 바뀜.
  ```

- Name Rules(이름 규칙)

  - 대소문자를 구별한다.(ex Spam 과 spam은 다르다.)
  - 반드시 문자나 underscore로 시작하고 숫자는 안됩니다.
  - 이름에 **.**이나 #로 시작하는 것은 지으면 안됩니다.

  ```python
  #Case1 - Worst  - 실행에는 문제 없지만 어려운 이름은 좋지 않아.
  adsadasd  = 35.0
  dpemdnlem = 12.50
  copdsadazc = adsadasd * dpemdnlem
  print(copdsadazc)
  
  #Case2 - Bad - good처럼 이해하기 쉬운 이름을 사용하는 것이 더 좋아
  a = 35.0 
  b = 12.50
  c = a * b
  print(c)
  
  #Case3 - Good - 이해하기가 너무 좋아!
  hours = 35.0
  rate = 12.50
  pay = hours * rate
  print(pay)
  ```

  

- Assignment Statements(대입문!)

  - 오른쪽 결과를 왼쪽 변수에 저장하는 것으로 구성되어 있음.

  ```python
  x = 0.6
  x = 3.9 * x * (1 - x)
  print(x) # 0.936 출력됨. 
            #3.9 * 0.6 * (1 - 0.6)
  x = 3.9 * x * (1 - x )
  print(x) # 0.2336256 출력됨. 
            #3.9 * 0.936 * (1 - 0.936)
  ```

##### Expressions(표현식)

- 연산자는 +(Addition), -(Subtraction), *(Multiplication), /(Division), **(power), %(Reminder), 등이 있음.
- 일반적으로 괄호 → 거듭 제곱 → 곱셉,나눗셈 → 덧셈,뺄셈 → 왼쪽에서 오른쪽으로 진행

##### Type (타입)

- 타입과 관련된  것은 예와 함께 정리하자면,

```python
mbc = 1 + 4
print(mbc) # 5로 출력됩니다.

sbs = 'hello ' + ' there'
print(sbs) # hello there로 출력됩니다.

sbs = sbs + 1 # 문자열 타입과 정수형 타입을 더하려 했기 때문에 에러가 발생합니다.

#타입 소개

sbs = 'hello' + ' world'
print(sbs) # hello world

type(sbs) # class 'str' 문자열 클레스 타입
type(1) # 정수 클레스 타입 - int!

#타입 예시와 변환 소개
k = 492
type( k ) # int 타입
b = float( k ) # float 타입으로 변환
print( b ) # 492.0으로 출력
type( b ) # float 타입
# int는 정수 타입이며, float는 부동 소수점 수 타입(실수 타입)

broadcast = '123' # '123'은 123과 다름!
type(broadcast) # str 타입
print(broadcast + 1) # 문자열(str)과 int를 더한 것이므로 오류

mymy = int(broadcast)
type(mymy) # int 타입
print(mymy + 1) # int 타입 간 연산이기 때문에 오류 발생하지 않는다. 124로 출력됨

#입력을 해보기
nam = input('Who are you? ') #Who are you? 라고 물어 볼 것이고 사용자는 입력값을 넣습니다.
print('Welcome', nam) # 해당 입력값을 nam이라는 변수에 할당한 다음 Welcome이라는 문자열과 함께 출력합니다. ex) sunny를 치면 Welcome sunny라고 나옴 

# #은 주석임 java의 //와 같음
```

##### 배운 내용 가지고 실습!

```python
nme = input('enter your name: ')
print("hello",nme)
# sunny를 입력하면 hello sunny라고 나온다.

xh = input("enter hours: ")
xr = input("enter rate: ")
xp = float(xh) * float(xr)
print("pay:", xp)
# 시간과 요금을 적으면 돈이 계산된다. 
# ex) 시간에 40, 요금에 9000을 입력하면 360000이 나온다.

a = 10 % 4 
print(a) # 2가 나옴

result = 3 + 4 / 4 * 4
print(result) # 7이 나옴

```

##### if와 else

- if

```python
# ex)
x = 4
if x < 10 : # if는 예약어이며, 컴퓨터는 if 다음에 나오는 조건문의 True, False를 판단함.
  print('Smaller') #만약 True인 경우 :(콜론) 아래로 들여쓰기 된 부분을 실행함. 
                       #여기서는 Smaller가 출력됨.
# if 뒤에 :(콜론) 꼭 써줘야함

#비교연산자에 대해서도 소개하자면 ,
# x>y - x가 y보다 큼, 만약 아니라면 false 
# x<y - x가 y보다 작음, 만약 아니라면 false
# x>=y // x<=y - x가 y보다 크거나 같음과 x가 y보다 작거나 같음, 아니라면 false
# == , != - ==은 같은 경우에 쓰이고 !=은 다른 경우에 쓰임, 아니라면 false

#들여쓰기
#ex)
x = 9
if x < 10:
print('small') #print가 들여쓰기 되지 않아 에러발생... 들여쓰기 안지키면 에러뜨니 주의!

```

##### if else

```python
#ex)
x = 15

if x < 10 :
    print('small')
else :
    print('big')
#여기서는 15가 10보다 크니까 if가 아닌 else로 쓰임, 따라서 big으로 출력함.
```

##### elif, try, except

- elif

```python
#ex)

x = 100

if x < 10 :
    print('Small')
elif x < 30 :
    print('Medium')
elif x < 50 :
    print('Big')
elif x < 70 :
    print('Large')
elif x < 90 :
    print('Huge')
else :
    print('Ginormous')

# Ginormous가 출력될 것임 그리고 만약에 x<70과 x<90이 반대로 되어있다면 Large는 절대 볼수 없으니 주의할 것!
```

- try / except
  - 에러를 대처하기 위한 좋은 예약어

```python
astr = "123"

try:
    print("Hello")
    isInt = int(astr)
    print("World")
except:
    isInt = "Integer로 변환할 수 없습니다."

print('Done', isInt)
# Hello
# World
# Done 123이 순서대로 출력됩니다.
# 올바른 값이 아니라면 에러가 발생하는데 except를 코드에 넣으면 해당 문구가 나옴.
```

##### 배운 내용 실습하기.

```python
# ex)
sh = input("enter hours: ") # 시간 입력
sr = input("enter rate: ") 	# 요금 입력
try:
    fh = float(sh)
    fr = float(sr)
except:
    print("Error, please enter numeric input") # 에러 발생을 예방하기 위함
    quit() # 끝내는 예약어

print(fh, fr)
if fh > 40 : #40시간이 넘은 경우 초과수당을 받을 때 사용함.
    reg = fr * fh
    otp = (fh- 40.0) * (fr * 0.5)
    xp = reg + otp
else: # 40이 안된다면 else로 적용되어 식이 계산될 것임.
    xp = fh * fr
print("Pay:", xp)

#ex2)
score = input("Enter Score: ") # 점수 입력

try:
    score = float(score)
except:
    print("Error, please enter numeric input") # 애러 대비 except
    quit()

if score > 1.0 :
    print("that`s out of range.") #1.0보다 크면 학점을 평가할 수 없음.
elif score >= 0.9 :
    print("A")
elif score >= 0.8 :
    print("B")
elif score >= 0.7 :
    print("C")
elif score >= 0.6 :
    print("D")
else:
    print("F") #0.6보다 낮으면 무조건 f임..
```





