### 파이썬 코딩 연습 



##### 점수를 입력하면 학점 출력하는 코딩

```python
score = input("Enter Score: ")

try: #try는 문제가 없을 시에 수행하는 것임.
    score = float(score)# float는 실수화.
except: # 문제가 있을 경우 해당 문구를 출력되고 종료됨.
    print("Error, please enter numeric input")
    quit()

if score > 1.0 :
    print("that`s out of range.") # 1.0이 기준이므로 그거보다 크면 에러임.
elif score >= 0.9 :
    print("A")
elif score >= 0.8 :
    print("B")
elif score >= 0.7 :
    print("C")
elif score >= 0.6 :
    print("D")
else:
    print("F")# 0.6보다 아래면 모두 f임.
```

