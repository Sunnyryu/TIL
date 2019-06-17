# Python( Watching PY4E Youtube)



#### 6.Basic

##### dictionary

- 컬렉션 부터 먼저 이해해보기
  - 한 가지 이상의 값을 넣고 한꺼번에 가지고 돌아다닐 수 있어서 편리함
  - 여러 개의 값을 하나의 “변수”에 담을 수 있음
  - 변수 “안”에 공간을 여러 개 가짐
  - 변수 안에서 서로 다른 공간을 찾는 방법이 있음
  - 컬렉션은 리스트와 딕셔너리로 나눔
    - 리스트는 순서를 유지하는 값들의 선형 컬렉션
    - 딕셔너리는 고유의 라벨을 갖고 있는 값을 넣는 “가방”

```python
# 컬렉션이 아님. 변수임
>>> x = 2
>>> x = 4
>>> print(x)
4
```

- 딕셔너리
  - 파이썬의 가장 강력한 데이터 컬렉션
  - 파이썬에서 빠르게 데이터베이스 같은 연산을 가능하게 함
  - 자바에서는 Hash Map, 속성, 맵,  php에서는 연관 배열과 비슷함
  - 순서가 없음
  - 조회 태그를 달아 인덱스를 매김

```python
#ex1)
purse = dict() # 또는 purse = {} 와 같이 생성할 수도 있습니다.
purse['cookies'] = 12 # 'cookies'라는 키에 12라는 값 연결
purse['candy'] = 3  # 'candy'라는 키에 3이라는 값 연결
purse['gum'] = 75 # 'gum'라는 키에 75라는 값 연결
print(purse) # 'cookies' : 12, 'candy' : 3, 'gum' : 75가 나옴
print(purse['gum']) # 75가농
#딕셔너리는 값과 키를 사용하는 것이고 리스트는 키 대신 숫자를 사용한다는 점에선 비숫함.
#ex2)>>> lst = list()
>>> lst.append(21)
>>> lst.append(183)
>>> print(lst)
[21, 183]
>>> lst[0] = 23
>>> print(lst)
[23, 183]
#리스트
>>> ddd = dict()
>>> ddd['age'] = 21
>>> ddd['course'] = 182
>>> print(ddd)
{'course': 182, 'age': 21}
>>> ddd['age'] = 23
>>> print(ddd)
{'course': 182, 'age': 23}
#딕셔너리

```

- 딕셔너리 표현
  - 딕셔너리는 중괄호로 표현하며 키 : 값 쌍 목록을 가짐
  - 사이가 비어있는 중괄호로 빈 딕셔너리를 만들 수 있음
- 카운팅
  - 대상이 얼마나 자주 보이는지를  셈
- 딕셔너리 에러
  - 없는 키를 입력할 때 Traceback 에러가 발생함
  - in 연산자를 사용하여 키가 딕셔너리에 있는지 확인 가능!
  - 새로운 것은 딕셔너리에 새로운 원소로 넣고 기존에 있던 것은 +1을 함
- 딕셔너리 get 메서드
  - 딕셔너리에 존재하는 키인지 아닌지 여부에 따라 처리하는 메서드

```python
#ex 1) 추가하기
ccc = dict()
ccc['abc'] = 1
ccc['efg'] = 1
print(ccc)
# {'abc': 1, 'efg': 1}
ccc['abc'] = ccc['abc'] + 1
print(ccc)
# {'abc': 2, 'efg': 1}

#ex 2) 에러의 예시
ccc = dict()
print(ccc['abc']) # 빈공간에 abc가 있는 지 확인하면 traceback 에러가 발생함.

#ex 3) in 연산자 이용
'abc' in ccc
# False 없으니까

counts = dict()
names = ['asd', 'sdf', 'asd', 'sdf', 'cwc']
for name in names :
    if name in counts: 
        counts[name] = counts[name] + 1
    else :
        counts[name] = 1
print(counts) #  {'asd': 2, 'sdf': 2, 'cwc': 1}

counts = dict()
names = ['asd', 'sdf', 'asd', 'sdf', 'cwc']
for name in names :
    if name not in counts: 
        counts[name] = 1
    else :
        counts[name] = counts[name] + 1
print(counts) #  {'asd': 2, 'sdf': 2, 'cwc': 1}

#ex 4) get 사용
counts = dict()
names = ['asd', 'sdf', 'asd', 'sdf', 'cwc']
for name in names :
    counts[name] = counts.get(name, 0) + 1
print(counts)
#get은 이름이 없다면 0으로 갖는 데이터를 추가하라고 하기에 에러가 발생되지 않음
# {'asd': 2, 'sdf': 2, 'cwc': 1} 
```

- 카운팅 패턴
  - 텍스트의 한 줄 안에 있는 단어 수를 셀 때, 일반적으로 split으로 나누어 루프에 넣음
  - 단어별로 수를 추적하기 위해 딕셔너리를 사용
  - split 메서드
    - 문자열에 split 메소드를 실행시키면 띄어쓰기를 기준으로 문장을 분할해 리스트를 만듬.
  - 유한 루프와 딕셔너리
    - 딕셔너리 안에는 저장되는 순서가 없다고 해도, for 문을 작성하여 딕셔너리의 모든 원소를 돌 수 있음 
    - 딕셔너리의 모든 키를 거쳐가며 값을 찾음
- items 메소드
  - 키와 값의 쌍을 얻기 위해 사용하며, 튜플이라는 자료 구조 안에 키와 값이 쌍을 지어 저장된 리스트가 반환됨

```python
#ex1) split
line = 'The general pattern to count the words'
print(line.split()) # 단어 단위로 쪼개줌

# ['The', 'general', 'pattern', 'to', 'count', 'the', 'words']

counts = dict() 
line = 'The general pattern to count the words in a line of text is to split the line into words, then loop through the words and use a dictionary to track the count of each word independently.'

words = line.split()

print('Words:', words)

# Words: ['The', 'general', 'pattern', 'to', 'count', 'the', 'words', 'in', 'a', 'line', 'of', 'text', 'is', 'to', 'split', 'the', 'line', 'into', 'words,', 'then', 'loop', 'through', 'the', 'words', 'and', 'use', 'a', 'dictionary', 'to', 'track', 'the', 'count', 'of', 'each', 'word', 'independently.']
# 문장이 길어도 동일하게 쪼개줌
for word in words:
    counts[word] = counts.get(word,0) + 1
print('Counts', counts)

# Counts {'The': 2, 'general': 2, 'pattern': 2, 'to': 6, 'count': 4, 'the': 8, 'words': 4, 'in': 2, 'a': 4, 'line': 4, 'of': 4, 'text': 2, 'is': 2, 'split': 2, 'into': 2, 'words,': 2, 'then': 2, 'loop': 2, 'through': 2, 'and': 2, 'use': 2, 'dictionary': 2, 'track': 2, 'each': 2, 'word': 2, 'independently.': 2}
#get을 이용하면 몇개가 나왔는 지도 구할 수 있음. 매우 유용함 !!!

# ex 2) 딕셔너리에 유한루프 적용하는 것
counts = { 'chuck' : 1 , 'fred' : 42, 'jan': 100}
for key in counts:
    print(key, counts[key])

# chuck 1
# fred 42
# jan 100

jjj = { 'chuck' : 1 , 'fred' : 42, 'jan': 100}
print(list(jjj))
# ['jan', 'chuck', 'fred']

jjj = { 'chuck' : 1 , 'fred' : 42, 'jan': 100}
print(jjj.keys())
# ['jan', 'chuck', 'fred'] 

jjj = { 'chuck' : 1 , 'fred' : 42, 'jan': 100}
print(jjj.values())
# [100, 1, 42] 값을 얻고 싶으면 밸류 메서드 사용!

# ex3 ) item method
jjj = { 'chuck' : 1 , 'fred' : 42, 'jan': 100}
for aaa,bbb in jjj.items() :
    print(aaa, bbb)

# chuck 1
# fred 42
# jan 100

# ex4) 활용
name = input('Enter file:')
handle = open(name)

counts = dict()
for line in handle:
    words = line.split()
    for word in words:
        counts[word] = counts.get(word,0) + 1

bigcount = None
bigword = None
for word,count in counts.items():
    if bigcount is None or count > bigcount:
        bigword = word
        bigcount = count

print(bigword, bigcount) #가장 많이 사용한 이름과 횟수가 출력됨

# ex5) 예제 풀어보기
fname = input('Enter file ')
if len(fname) < 1 : fname = 'clown.txt'
hand = open(fname)

di = dict()
for lin in hand:
  lin = lin.rstrip()
  # print(lin)
  wds = lin.split()
  print(wds)
  for w in wds:
      # if the key is not there the count is zero
      #print('**',w,di.get(w,-99))
      #oldcount = di.get(w,0)# 위에있는 if the key 역활을 이것이함
      # idiom : retieve/ create / update counter
      #print(w,'old',oldcount)
      #newcount = oldcount + 1
      #di[w] = newcount

      di[w] = di.get(w,0) + 1
     # print(w,'new',newcount)
     # if w in di :
          #di[w] = di[w] + 1
         # print('**Existing**')
     # else :
         # di[w] = 1
         # print(w,di[w])
         # print('**NEW**')
#print(di[w])

# now we want to find the most common word
largest = -1
theword = None

for k,v in di.items() :
    #print(k,v)
    if v > largest:
        largest = v
        theword = k #cature/remember the word that was largest

print(largest, theword) # 가장 많이 나온 단어와 횟수가 나옴.
```









