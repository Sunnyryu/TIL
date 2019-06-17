Python( Watching PY4E Youtube)



#### 7.Basic

##### Tuple

- 튜플은 리스트와 비슷한 기능을 하는 시퀀스

```python
#ex 1)
x = ('Hyunsun', 'Sunny', 'Tom')
print(x[2])
# Tome
y = ( 1, 2, 3 )
print(y)
# (1, 2, 3)
print(max(y))
# 3
```

- 리스트와 다르게 변경이 불가능하다.
- 그렇기 때문에 리스트보다 효율적이며, 용량도 적게 차지하고 접근도 편하다.
  - 그러나 리스트에서 하지 못하는 것은 튜플에서 하지 못하는 것도 있음
- 튜플은 임시 변수로 활용할 수 있다.

```python
# ex 1)
(x, y) = (4, 'fred')
print(y)
# fred
(a, b) = (99, 98)
print(a)
# 99 , 좌변과 우변이 일정해야 함.

# ex 2)
def t() :
    return (10, 20)
x, y = t()
print(x, y)
# 10 20
# ex 3)
x, y = 1, 10
print(x, y)
# 1 10

x, y = y, x
print(x, y)
# 10 1
```

- 딕셔너리를 처리하는 데 활용 할 수 있음

```python
#ex 1)
d = dict()
d['abc'] = 2
d['def'] = 4
for (k,v) in d.items(): 
    print(k, v)
# abc 2
# def 4

tups = d.items()
print(tups)
# dict_items([('abc', 2), ('def', 4)])
```

- 여러 값에 대해 비교가 가능하다.

```python
# ex 1)
 (0, 1, 2) < (3, 1, 2)
# True 값을 가집니다. 가장 왼쪽부터 비교.
 (0, 1, 1000000) < (0, 5, 6)
# True 값을 가집니다. 가장 왼쪽이 같으면, 두 번째 자리 비교.
 ( 'Ryu', 'Hyunsun' ) < ('Ryu', 'Hyunzun')
# True 값을 가짐 s< z
 ( 'Ryu', 'Hyunsun' ) < ('Hyunsun', 'Ryu')
# True 값을 가집니다. R > H
```

- 키를 기준으로 정렬할 수 있음

```python
# ex 1)
>>> d = {'b':10, 'a':9, 'c':11}
>>> d.items()
dict_items([('b', 10), ('a', 9), ('c', 11)])
>>> sorted(d.items())
[('a', 9), ('b', 10), ('c', 11)]
# ex 2)
for k, v in sorted(d.items()):
    print(k, v)
# a 9
# b 10
# c 11

# ex 3)
c = {'a':91, 'b':10, 'c':77}
tmp = list()
for k, v in c.items() :
    tmp.append( (v, k) ) # k와 v를 v와 k로 바꿔줌

print(tmp)
# [(91, 'a'), (10, 'b'), (77, 'c')]
tmp = sorted(tmp) # sorted를 사용하면 오름차순 정렬이 됩니다.
print(tmp)
# [(10, 'b'), (77, 'c'), (91, 'a')]

# ex 4)
c = {'a':91, 'b':10, 'c':77}
tmp = list()
for k, v in c.items() :
    tmp.append( (v, k) )

print(tmp)
# [(91, 'a'), (10, 'b'), (77, 'c')]
tmp = sorted(tmp, reverse=True) # reverse = true면, 내림차순으로 정렬한다.
print(tmp)
# [(91, 'a'), (77, 'c'), (10, 'b')]
```

- 리스트 컴프리헨션은 동적인 리스트를 생성함.

```python
# ex 1 )
c = {'a':91, 'b':10, 'c':77}
print( sorted( [ (v,k) for k,v in c.items() ] ) )
# [(10, 'b'), (77, 'c'), (91, 'a')]
```

- 예시로 이해해보기

```python
abc = open('xyz.txt')
counts = {}
for line in abc:
    words = line.split() # 스플릿을 사용하여 쪼개줌
    for word in words:
        counts[word] = counts.get(word, 0 ) + 1 # 카운트가 늘어나면 +1을 해줌

lst = []
for key, value in counts.items():
    newtup = (value, key) # key와 value를 바꿔줌
    lst.append(newtup) 

lst = sorted(lst, reverse=True)

for value, key in lst[:10] : # 가장 많은 10가지를 뽑아낼 수 있음.
    print(key, value)
```













