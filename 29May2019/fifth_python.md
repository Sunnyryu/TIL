# Python( Watching PY4E Youtube)



#### 5.Basic

##### 리스트	

- 알고리즘
  - 문제를 해결하는 데 사용하는 일련의 규칙 또는 단계
- 자료 구조
  - 컴퓨터에서 자료를 구성하는 특별한 방법 
- 컬렉션
  - 컬렉션이 아닌 것은 예를 들어, 변수가 한가지 값을 갖을 때 다른 값을 넣어 지워질 때
  - 컬렉션은 하나의 변수에 많은 것을 넣을 수 있음
  - ex) games = ['starcraft', 'warcraft', 'league of legends']
- 리스트 상수
  - 대괄호로 둘러싸여 있고 리스트의 원소는 반점으로 구분됨.
  - 파이썬의 어떤 객체도 원소를 넣을 수 있음.(다른 리스트도 넣을 수 있음)
  - 빈 리스트도 생성할 수 있음

```python
#ex 1)
print([1, 2, 3 ])
[1, 2, 3]
print([100, 98.6, red, [77, 66]])
[100, 98.6, red, [77, 66]]
# ex 2)
for i in [6, 5, 4, 3, 2, 1] : #  5 4 3 2 1 Blassoff!로 하나씩 출력됨
    	print(i)
    print('Blastoff!')
#ex 3)
games = ['fifa', 'wwe', 'nba'] # i played the fifa / i played the wwe/ i played the nba/done! 으로 출력됨
for game in games 
	print('i played the', games)
print('done!')

    
```

- 리스트의 내부

  - 문자열과 마찬가지로, 대괄호를 이용한 인덱스로 리스트의 원소를 하나하나를 가져나올 수 있음 

- 리스트는 변경 가능, 문자열은 변경 불가

  - 리스트는 인덱스 연산자를 사용하여 리스트의 요소를 변경 가능

- 리스트의 길이를 구할 떄는 len()함수를 이용함

  - len() 함수는 리스트를 매개변수로 받으며, 리스트의 원소 개수를 변환함
  - len() 함수는 아무 집합이나 시퀀스(ex:문자열) 를 받아 원소의 개수를 반환함

  ```python
  # ex 1)
  greet = "hello Sunny"
  print(len(greet))
  # 9
  x = [1,2, 'ryu', 88]
  print(len(x))
  # 4
  ```

- range 함수

  - 0부터 매개변수까지 넣은 값보다 1 작은 범위 수까지 구성된 숫자 리스트를 반환
  - for 문과 정수 반복자를 통해 인덱스 루프를 구성 가능

```python
#ex 1) 
print(range(4))
[0, 1, 2, 3]
friends = ['sunny', 'huni', 'honi']
>>> print(len(friends))
3
>>> print(range(len(friends)))
[0, 1, 2]
# ex 2)
friends = ['sunny', 'huni', 'honi']
for friend in friends :
print('Happy New Year:', friend)
for i in range(len(friends)) :
friend = friends[i]
print('Happy New Year:', friend)
# Happy New Year sunny
# Happy New Year huni
# Happy New Year honi
```

- +와 :를 사용할 수 있음
  - +를 사용하여 리스트를 연결할 수 있음 (a = [1, 2] b= [3, 4] c = a+b => [1, 2, 3, 4])
  -  :를  사용하여 리스트를 자를 수 있음(a = [1, 2, 3, 4])
    - a[1:3] = [2, 3], a[:3] = [1, 2, 3], a[:] = [1, 2, 3, 4]
- 리스트 메서드

```python
x = list()
type(x)
<type 'list'>
dir(x)
['append', 'count', 'extend', 'index', 'insert',
'pop', 'remove', 'reverse', 'sort']
# 위의 있는 것들을 다 사용할 수 있음.!
```

- append
  - append를 이용하면 빈 리스트나 리스트에 추가할 수 있음
    - ex a = list()가 비었을 때 a.append(100)을 하면 print(a) = [100]이 됌
- 리스트 원소 탐색
  - 파이썬은 특정 원소가 리스트에 있는지 확인할 수 있는 두 가지의 연산자를 제공함
  - 둘 다 참과 거짓을 반환하는 논리 연산자
  - 리스트를 바꾸지는 않음
- 리스트에는 순서가 있음
  - 많은 아이템 보관 가능, 아이템의 순서가 일반적으로 유지
    - sort를 이용하면 스스로 정렬하는 기능이 사용됨

- 내장함수와 리스트
  - 리스트를 매개 변수로 받는 내장 함수가 여러 가지 있음
    - ex) len, max, min, sum 등
- 문자열과 리스트 
  - split 함수는 문자열을 작게 나누고 문자열로 구성된 리스트를 생성
  - 특정 단어에 접근하거나 모든 단어에 대해 루프를 실행할 수 있음
  - 구획문자를 별도로 설정하지 않으면 공백을 기준으로 나눔(split 함수)
  - 문장을 나눌 떄 어떤 것을 기준으로 나눌 지 사용하여 정하기 가능(ex: split(;))
- 이중으로 나누는 패턴
  - 문장을 하나의 구획 문자로 나누고 그 조각 중 일부를 다시 다른 구획 문자로 나누는 패턴



​		







