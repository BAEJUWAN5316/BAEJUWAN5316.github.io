---
layout: post
title: "Pyhthon 문제풀이1"
--- 
# 문제
### 학생 이름과 점수가 담긴 딕셔너리 scores가 주어질 때, 가장 점수가 높은 학생의 이름을 return 하도록 solution 함수를 완성하세요.

## [ 조건 ]
딕셔너리의 key는 문자열(이름), value는 정수(점수),
최고 점수를 받은 학생이 여럿일 경우 아무나 리턴,

## [ 풀이 방식 ]
max() 함수와 lambda를 사용하여 구하기

```python
scores = {"철수": 85, "영희": 92, "민수": 78, "영지": 88}

def solution():
    result1 = scores.items()
    result1 = list(result1)
    return max(result1, key=lambda x: x[1])[0]

print(solution())
```

1. items로 키와 값을 튜플 형태로 묶는다.
2. 튜플을 리스트 형태로 바꾼다
3. 리스트의 값들을 max함수로 정렬할 건데 기준을 1번째 인덱스를 기준으로 하기 위해 lambda를 사용했다.
4. max의 반환값은 튜플형태이므로 이름을 출력하기 위해 0번째 인덱스를 추출하여 solution함수의 reutrn값으로 둠
5. 출력시 "영희" 출력.
6. 점수 값을 바꿔도 가장 높은 값의 이름이 출력된다.
