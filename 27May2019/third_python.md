# Python( Watching PY4E Youtube)



#### 3.Basic

##### 문자열

- 문자열 
  - 문자열을 예를 들어 이해해보자면,

```python
# ex1)
name = input('Enter: ') # 예를 들어 555를 입력
print(type(name)) # 입력한 555의 타입은 <class 'str'>과 같음
print(name)# 555가 출력

# ex2)
fruit = 'apple' # a부터 0이고 e는 4이다. a=0, p=1, p=2, l=3, e=4 
letter = fruit[0] # letter는 fruit의 0이므로 
print(letter)# a가 출력됨.
letter = fruit[1] # letter는 fruit의 1이므로
print(letter) # p가 출력됨
letter = fruit[2] # letter는 fruit의 2이므로
print(letter) # p가 출력됨

# ex3)
fruit = 'apple'
print(len(fruit)) # len 함수는 문자열의 길이를 알 수 있게 해주는 함수입니다.
# apple은 5글자이므로 5가 출력됨.

# ex4)
fruit = 'apple'
index = 0

# while 루프

while index < len(fruit) : # index가 len(fruit)보다 작지 않을 때까지 무한 반복
    letter = fruit[index] 
    print(index, letter) # 0 a, 1 p, 2 p, 3 p,4 l,5 e로 출력됨 
    index = index + 1
    
# for 반복문
for letter in fruit :
    print(fruit[0:], letter)


```

- 문자열 슬라이싱
  - 특정 문자열을 가져올 수 있는데, 예를 들자면,

```python
#ex1)
myString = 'Monty Python'
print(myString[0:4])
# Mont가 출력됩니다. 여기서 0 to 4에서 4에 대한 인덱스는 출력되는 값에 포함되지 않는 것을 확인하여야함.
print(myString[6:7])
# P가 출력됨.
print(myString[6:20])
# Python이 출력됨.
print(myString[:2])
# index값이 2에 해당하는 문자 앞까지 출력됨.
print(myString[8:])
# index값이 8에 해당하는 문자부터 출력됨.
print(myString[:])
# 전체가 출력됨
#ex2)
firstString = 'Hello'
secondString = 'There'
print(firstString + secondString)
# HelloThere로 출력됩니다.
thirdString = firstString + ' ' + secondString
print(thirdString)
# Hello There로 출력됩니다.

#ex)3 반복문 응용하기.
fruit = 'banana'
print('n' in fruit)
# True로 출력됨
print('m' in fruit)
# False로 출력됨
print('nan' in fruit)
# True로 출력됨
if 'a' in fruit :
    print('Found it!')
# Found it으로 출력됨

# ex 4) 
greet = '                     Hello Hyunsun       '
greet.lstrip()
# 왼쪽의 공백이 삭제됨 (lstrip()은 왼쪽 공백 삭제)
greet.rstrip()
# 오른쪽의 공백이 삭제됨(rstrip()은 오른쪽 공백 삭제)
greet.strip()
# 양쪽의 공백이 삭제됨(strip() 양쪽 공백 삭제 )

# ex 5)
line = 'Please have a nice day'
print(line.startswith('Please'))
# True가 출력됨
print(line.startswith('p'))
# False가 출력됨 : 대소문자 구분 (P로 써야 출력됨)

#ex 6)
str = 'X-DSPM-Confidence: 0.8475'

ipos = str.find(':') # : 앞까지 총 18개
piece = str[ipos+2:] # ipos 뒤에 2칸 부터 끝까지임.
value = float(piece) # 실수화가 됨.
print(value) # 0.8475가 나옴.

```









