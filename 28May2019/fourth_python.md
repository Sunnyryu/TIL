# Python( Watching PY4E Youtube)



#### 4.Basic

##### 파일

- 텍스트 파일
  - 텍스트 파일은 연속적으로 연결되어 있는 줄글의 집합이라고 생각하면 됌.
- open()
  - 파일을 여는 것은 open() 함수를 이용하며, open() 함수는 handle을 반환하게 되고 handle은 파일에 대한 작업을 수행하기 위해 사용됨. handle은 텍스트가 파일 형태, 메모리에 저장된 문자열의 형태, 웹 사이트에서 존재하는 형태와 같이 다른 방식으로 저장되어 있는 텍스트를 처리하는 하나의 표준화된 방식임. 예를 들어보자면

```python
# ex1)
fhand = open('abc.txt', 'r')

# open('파일명입력', '모드 선택')
# 1. 파일명 입력
# 파일명은 문자열 타입으로 입력하며, 확장자까지 포함시켜 줍니다.
# 2. 모드 선택
# 모드에서는 w 또는 r 두가지를 선택할 수 있습니다. 'w'는 파일을 작성할 때 사용하며, 'r'은 파일을 읽을 때 사용함.
```

- 개행문자 
  - \n이라고 하며, 행을 바꾸는 문자임. 파이썬에서 \n은 하나의 문자임. 예를 들어보자면,

```python
#ex1)
stuff1 = 'Hello Sunny!'
print(stuff1) # Hello Sunny!
print(len(stuff1)) # 12
stuff2 = 'Hello\nSunny!'
print(stuff2)   # Hello
				# Sunny!
print(len(stuff2)) # 12

```

- 파일핸들
  - 순서가 있고 연속적으로 구성된 텍스트 파일을 한줄한줄 읽어 나감. 예를 들자면,
  - 텍스트 파일을 읽는 하나의 표준화된 형태임.

```python
#ex1)
fhand = open('sub.txt')

for line in fhand :
    print(line)

# 다음을 출력하게 되면 한줄씩 띄워져서 출력되게 됨.
#ex2)
fhand = open('sub.txt')
count = 0

for line in fhand :
    count = count + 1
print('Line Count: ', count)

# 만약에 line Count가 35라면 Line Count:  35로 출력됨.
#ex3)
fhand = open('mbox-short.txt')
inp = fhand.read()
print(len(inp))
# 만약에 inp의 길이가 94646라면 94646으로 출력됨.
print(inp[:20])
# ex) From stephen.marquar으로 출력됨.

#ex4)
fhand = open('mbox-short.txt')
for line in fhand:
    line = line.rstrip() # 오른쪽 공백 제거
    if line.startswith('From:') :
        print(line)
   #만약에 개행문자가 있다면 rstrip으로 인해 제거 되어 출력됨.
#ex5)
fname = input('Enter the file name:  ')
try:
    fhand = open(fname)
except:
    print('File cannot be opened: ', fname)
    quit()

count = 0
for line in fhand:
    if line.startswith('Subject:') :
        count = count + 1
print('There were', count, 'subject lines in', fname)

# There were 27 subject lines in mbox-short.txt와 같이 출력됨. 그리고 위에서는 에러를 방지하기 위해 try, except를 사용함.

```









