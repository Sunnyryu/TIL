Python( Watching PY4E Youtube)



#### 8.Basic

##### 정규식

- 텍스트에서 특정 글자나 단어, 패턴 등을 정확하고 유동적으로 표현하는 식임.
- 문자열 비교나 처리를 위한 아주 똑똑한 와일드 카드 표현식(다른 의미)
- 기호로 되어 있어 굉장히 효과적이지만 조금 어려움
- 한 번 배우면 활용할 곳이 많음
- 정규식은 자체로도 언어임
- 특수문자로 이루어진 언어로 문자만을 사용해서 프로그래밍을 하는 개념
- 축약된 '형식 언어'의 종류

```python
# ex)
# ^ Matches the beginning of a line (라인의 시작 매칭)
# $ Matches the end of the line (라인의 끝을 매칭)
# . Matches any character)(임의 문자 매칭 - 와일드 카드)
# \s Matches whitespace(공백 문자 매칭)
# \S Matches any non-whitespace character(공백이 아닌 문자 매칭)
# * Repeats a character zero or more times(바로 앞선 문자에 적용되고 0 혹은 그 이상의 앞선 문자와 매칭을 표기)
# *? Repeats a character zero or more times (non-greedy) ( 바로 앞선 문자에 적용되고 0 혹은 그 이상의 앞선 문자와 매칭을 탐욕적이지 않은 방식으로 표기)
# + Repeats a character one or more times ( 바로 앞선 문자에 적용되고 1 혹은 그 이상의 앞선 문자와 매칭을 표기)
# +? Repeats a character one or more times (non-greedy) ( 바로 앞선 문자에 적용되고 1 혹은 그 이상의 앞선 문자와 매칭을 탐욕적이지 않은 방식으로 표기함.)
# [aeiou] Matches a single character in the listed set ( 명세된 집합 문자에 존재하는 단일 문자와 매칭. “a”, “e”, “i”, “o”, “u” 문자만 매칭되는 예제)
# [^XYZ] Matches a single character not in the listed set ( 기호로 문자 범위를 명세할 수 있다. 소문자이거나 숫자인 단일 문자만 매칭되는 예제)
# [a-z0-9] The set of characters can include a range
# ( Indicates where string extraction is to start
# ) Indicates where string extraction is to end
# 괄호가 정규표현식에 추가될 때, 매칭을 무시한다. 하지만 findall()을 사용 할 때 전체 문자열보다 매칭된 문자열의 상세한 부속 문자열을 추출할 수 있게 한다.
```

- 정규식 모듈
  - 정규식을 사용 하기 전에 "import re" 명령어로 라이브러리를 불러옴.
  - re.search() 를 사용하면 find() 메소드를 쓴 것처럼 정규식에 매칭되는 문자열을 찾을 수 있음
  - re.findall() 을 사용하면 정규식에 맞는 문자열 추출 가능 (find() 와 slicing: var[5:10] 을 조합한 것과 유사)

```python
# ex 1)정해진 문자를 추가하여 문자열에 어떻게 매치되는지를 조절
hand = open('mbox-short.txt')
for line in hand:
line = line.rstrip()
if line.find('From:') >= 0:
print(line)
import re
hand = open('mbox-short.txt')
for line in hand:
line = line.rstrip()
if re.search('From:', line) :
print(line)

#ex 2)
import re

hand = open('mbox-short.txt')
for line in hand:
    line = line.rstrip()
    if line.startswith('From:') :
        print(line)
        
import re

hand = open('mbox-short.txt')
for line in hand:
    line = line.rstrip()
    if re.search('^From:', line) :
        print(line)
```

- 특수 지정 문자
  - 점(.) 문자는 어떤 문자가 와도 상관없다는 뜻
  - asterisk(*) 문자는 몇 번 와도 상관없다는 뜻
- 매칭 시키기
  - 데이터가 얼마나 잘 정리되어 있는지와 어떻게 사용할지에 따라서 매치를 적절하게 사용
    - ^X.*: ( X로 시작하며(^) 아무문자(.)나 몇번(곱하기 기호())'이든 올수 있다는 뜻임)
    - ^X-\S+:(X로 시작하며 -가 들어가고 공백을 제외한(\S) 모든 것이 한번 이상(+) 반복 가능)
    - ^F.+: : F로 시작하며, 하나이상 반복하며, 마지막 문자는 :
    - ^F.+?: : F로 시작하며, 하나이상 반복하며, 가장 짧게, 마지막 문자는 :
- 매칭과 데이터 추출
  - re.search()는 해당 문자열이 대상 정규식을 만족시키는지를 True/False로 리턴
  - 매칭된 문자열을 추출하고 싶으면 re.findall() 을 사용
    - ex) [0-9]+ (0부터 9까지 반복 가능)

```python
#EX 1)
import re
x = 'My 2 favorite numbers are 19 and 42'
y = re.findall('[0-9]+',x)
print(y)
['2', '19', '42']

import re
x = 'My 2 favorite numbers are 19 and 42'
y = re.findall('[0-9]+',x)
print(y)
['2', '19', '42']
y = re.findall('[AEIOU]+',x)
print(y)
[]

y = re.findall('\S+@\S+',x) # 한개 이상의 빈칸이 아닌 문자.
print(y)
['stephen.marquard@uct.ac.za’]
 #EX 2)
# From stephen.marquard@uct.ac.za Sat Jan 5 09:14:16 2008
 
 data = 'From stephen.marquard@uct.ac.za Sat Jan 5 09:14:16 2008'
>>> atpos = data.find('@')
>>> print(atpos)
21
>>> sppos = data.find(' ',atpos)
>>> print(sppos)
31
>>> host = data[atpos+1 : sppos]
>>> print(host)
uct.ac.za
 
 line = 'From stephen.marquard@uct.ac.za Sat Jan  5 09:14:16 2008'
words = line.split()
email = words[1]
pieces = email.split('@')
print(pieces[1])
# at(@) 표시가 나올 때까지 string을 탐색
# 'uct.ac.za'
 
 import re 
lin = 'From stephen.marquard@uct.ac.za Sat Jan  5 09:14:16 2008'
y = re.findall('@([^ ]*)',lin)
print(y)
# Blank가 아닌 Character와 Match 몇 개든 제한 없음
# ['uct.ac.za'] , 중간에 ^이 들어가면 뒤를 제외한다는 것임
 
 import re 
lin = 'From stephen.marquard@uct.ac.za Sat Jan  5 09:14:16 2008'
y = re.findall('^From .*@([^ ]*)',lin)
print(y)
#문자열의 시작 점을 찾는데, 'From ' 으로 시작하는 것을 검색
 #다른 캐릭터는 모두 통과(*), @표시를 검색
 #'^From .*@([^ ]+)' 공백이 아닌 문자열 1개 이상이면 다 해당
 #'^From .*@([^ ]+)' 추출 종료 
# ['uct.ac.za']
```

```python
import re
hand = open('mbox-short.txt')
numlist = list()
for line in hand:
    line = line.rstrip()
    stuff = re.findall('^X-DSPAM-Confidence: ([0-9.]+)', line)
    if len(stuff) != 1 :  continue
    num = float(stuff[0])
    numlist.append(num)
print('Maximum:', max(numlist))

# SPAM 감지

# 예외문자는 지정된 특수 문자를 그냥 문자 그대로 그대로, 사용하고 싶을 경우 대부분 '\'를 붙이면 됨.
import re
>>> x = 'We just received $10.00 for cookies.'
>>> y = re.findall('\$[0-9.]+',x)
>>> print(y)
['$10.00']
#\$[0-9.]+ $= 그냥 S , [0-9.] = 0~9 숫자 또는 ., + 1개이상
```

