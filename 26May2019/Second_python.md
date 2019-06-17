# Python( Watching PY4E Youtube)



#### 2.Basic

##### 반복문

- While 반복문
  - while 반복문에 대해서 예를 들어보자면,

```python
#ex1)
n = 5 # n을 선언해줌.

while n > 0: #n이 0보다 크다면 반복 (5.4.3.2.1)
    print(n)
    n = n - 1

print('Blastoff!')
print(n) #5,4,3,2,1,;Blasftoff!가 나올 것임.
#ex)2
while True: # 무한루프가 걸릴 수 있음
    line = input('> ') # 입력하면 반복되는데, 밑의 break로 무한루프의 탈출조건을 설정.
    if line[0] == '#' :
        continue # #이 들어가는 것을 입력하면 해당루프는 
    if line == 'done' : # 종료 후에 루프 시작 지점으로 돌아감.
        break # done을 치면 while문을 나와서 바로 뒤를 실행
    print(line)
print('Done!')

# > hello there 입력
# hello there로 출력
# # don't print this '#'을 입력하게 되면 continue를 만나게 되고 continue는 loop의 시작점으로 다시 돌아가서 loop를 실행하게 됩니다.
# > print this! 입력
# print this!로 출력
# > done 입력
# Done!으로 출력 done을 입력하게 되면 break를 만나게 되고 break는 loop끝나는 점 바로 다음에 오는 코드를 실행하게 됩니다.
 
```

- for 문
  - 일반적으로 유한 개의 항목들에 대해 특정 반복을 하려고 할 때 많이 씀.
  - 예를 들어 설명해보자면,

```python
#ex1)
friends = ['Connect', 'Korea', 'Incheon'] 
for friend in friends: # connect, korea, Incheon을 반복하여 출력.
    print('Happy New Year!! ', friend)# Happ new Year!! connect,
print('Done!') # Happy new year!! korea, Happy new year!! Incheon이 출력
#ex2)
largest_so_far = -1 # -1로 선언
print('Before', largest_so_far) # 현재 호출된 값 확인을 위한 프린트
numbers = [9, 41, 12, 3, 74, 15] 
for the_num in numbers :
    if the_num > largest_so_far : 
        # iteration value의 현재의 값(the_num)이 현재 가장 큰 값이 할당 되어 있는 
        # largest_so_far보다 크다면 largest_so_far의 값을 the_num으로 바꿔줍니다.
        largest_so_far = the_num
    print('largest_so_far: ', largest_so_far, 'current number: ',the_num)
print('After', largest_so_far) # After 74로 호출됨.

#ex)3 반복문 응용하기.
count = 0 # count 선언
sum = 0 # sum 선언
print('Before', count, sum)
numbers = [9, 41, 12, 3, 74, 15] 
for value in numbers : # for 문을 이렇게 사용함..
    count = count + 1
    sum = sum + value
    print(count, sum, value)
print('After', count, sum, sum/count) # After 6 154 25.6666666으로 나옴.

found = False #found를 False로 선언
print('Before', found)# 현재값 확인
numbers = [9, 41, 12, 3, 74, 15]
for value in numbers :
    if value == 3 :# 3이 되기 전까지는 false, 3이면 True로 호출됨.
        found = True
        print(found, value)
        break # 특정 값을 찾으면 반복문 종료.
print('After', found) # After True

# ex 4) for, while 문제 풀어 이해해보기.
num = 0
tot = 0.0
while True :
    ohyes = input('Enter a number:') # 숫자 입력
    if opid == 'done' : # done이면 break로 반복문 빠져나옴
        break
    try: # try는 문제가 없으면 그냥 진행.
       opid = float(ohyes) # 부동 소수점으로 바꿔줌
    except: # 문제가 있으면 해당 except 진행
        print('Invalid input') # 호출
        continue # 빠져나간 후에 처음 루프로 돌아감.

    num = num + 1
    tot = tot + opid

print(tot,num,tot/num)

largest = None # 선언
smallest = None # 선언
while True:
    num = input("Enter a number: ")# 입력
    if num == "done" :# done을 입력하면 break
        break
    try:
        inum = int(num) # int로 변환
    except:
        print('Invalid input') #에러 발생 시 처음 루프로 돌아감
        continue
    if largest is None: #if 문 이용하여 진행
        largest = inum
    elif largest < inum : 
        largest = inum
    if smallest is None:
        smallest = inum
    elif smallest > inum :
        smallest = inum
print("Maximum is", largest) 
print("Minimum is", smallest)
# 10,7,2,5,best,done을 입력하면.
# Invalid input와 Maximum is 10과 Minimum is 2가 출력됨.
```









