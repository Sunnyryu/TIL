### 파이썬 코딩 연습 



##### 시간이 얼마나 출력하기 위한 문제

```python
fname = input('Enter file ')
if len(fname) < 1 : fname = 'mbox-short.txt'
hand = open(fname)

di = dict()
for lin in hand:
  lin = lin.rstrip()
  if lin.startswith('From:') :
      continue # From:이 들어간 것은 출력을 안 시키기 위해
  if lin.startswith('From') :
      # print(lin)
      wds = lin.split()
      wds = wds[5:6]
      # print(wds)
      for wds2 in wds :
          wds2 = wds2.rstrip() # 공백 제거
          wds3 = wds2[0:2]
          # print(wds3), 0~1 까지만 뽑아냄 ex) 16:01:02면 16만 뽑아냄.
          di[wds3] = di.get(wds3,0) + 1
          # print(di)
wds4 = sorted(di.items())
for k,v in wds4 :
    print(k,v)
```

