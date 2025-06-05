# 이동하는 별 게임 만들기!

### 5 X 5 의 좌표를 만들고 방향을 입력하면 별을 이동시키며 이동 횟수에 따라 다른 메세지를 출력하는 게임을 만들어보자!

```python
line1 = [["☆ ","☆ ","☆ ","☆ ","☆ "],
        ["☆ ","☆ ","☆ ","☆ ","☆ "],
        ["☆ ","☆ ","★ ","☆ ","☆ "],
        ["☆ ","☆ ","☆ ","☆ ","☆ "],
        ["☆ ","☆ ","☆ ","☆ ","☆ "],]
moved_star = 0
while True:
    print("")
    print("".join(line1[0]))
    print("".join(line1[1]))
    print("".join(line1[2]))
    print("".join(line1[3]))
    print("".join(line1[4]))
    move1 = input("움직일 방향을 선택하세요. [4.좌/6.우/8.상/2.하/0.나가기]")
    x = 0
    y = 0
    for star_y in range(5):
        for star_x in range(5):
            if line1[star_y][star_x] == "★ ":
                x = star_x
                y = star_y
    
    if move1 == "6":
        if x == 4:
            print("우측으로 더이상 움직일 수 없습니다.")
        else:
            line1[y][x] = "☆ "
            line1[y][x+1] = "★ "
            moved_star += 1
    elif move1 == "4":
        if x == 0:
            print("좌측으로 더이상 움직일 수 없습니다.")
        else:
            line1[y][x] = "☆ "
            line1[y][x-1] = "★ "
            moved_star += 1
    elif move1 == "8":
        if y == 0:
            print("위쪽으로 더이상 움직일 수 없습니다.")
        else:
            line1[y][x] = "☆ "
            line1[y-1][x] = "★ "
            moved_star += 1
    elif move1 == "2":
        if y == 4:
            print("아래쪽으로 더이상 움직일 수 없습니다.")
        else:
            line1[y][x] = "☆ "
            line1[y+1][x] = "★ "
            moved_star += 1
    elif move1 == "0":
        break
    else:
        print("올바른 방향을 입력해주세요.")

print(f"\n별의 이동 횟수: {moved_star}")
if moved_star >= 20:
    print("별은 뜨겁게 활활 타오릅니다!")
elif moved_star >= 15:
    print("별은 뜨거워졌습니다!")
elif moved_star >= 10:
    print("별에는 온기가 돕니다..!")
elif moved_star >= 5:
    print("별은 아직 차갑습니다...")
elif moved_star >= 3:
    print("별의 곳곳에 얼음이 보입니다...")
elif moved_star == 0:
    print("별에게는 아무 일도 일어나지 않았습니다...")
```

완성코드입니다!

### * 시작 전
방향키 입력 시 별이 이동하고, 이동 된 화면을 출력하기 위해 
while True 구문을 사용해준다.

### 1. 입력내용 만들기
```python
line1 = [["☆ ","☆ ","☆ ","☆ ","☆ "],
        ["☆ ","☆ ","☆ ","☆ ","☆ "],
        ["☆ ","☆ ","★ ","☆ ","☆ "],
        ["☆ ","☆ ","☆ ","☆ ","☆ "],
        ["☆ ","☆ ","☆ ","☆ ","☆ "],]
moved_star = 0
while True:
    print("")
    print("".join(line1[0]))
    print("".join(line1[1]))
    print("".join(line1[2]))
    print("".join(line1[3]))
    print("".join(line1[4]))
    move1 = input("움직일 방향을 선택하세요. [4.좌/6.우/8.상/2.하/0.나가기]")
```
인덱스를 y, x좌표로 지정할 수 있도록 이중리스트를 만들어준다.
그리고 실행 시 별 모양이 보일 수 있도록 join메서드를 이용해준다.
또한 input을 이용하여 별의 이동 방향 및 exit를 만들어 준다.


### 2. 좌표 생성하기
```python
x = 0
y = 0
    for star_y in range(5):
        for star_x in range(5):
            if line1[star_y][star_x] == "★ ":
                x = star_x
                y = star_y
```
우선 기본 값으로 x와 y좌표를 0으로 지정해준다.
for in 구문을 사용하여 x, y좌표의 인덱스 값인 0~4가 각각 들어가게 해준다
그럼 [1][0], [2][0], ... [3][4], [4][4] 식으로 좌표를 순회하게 되고,
검은 별의 좌표가 찾아졌을 때 변수 x와 y 좌표값에 입력이 되도록
if 구문을 사용하여 조건을 걸어준다.

### 3. 방향 입력에 맞추어 별 이동시키기
```python
    if move1 == "6":
        if x == 4:
            print("우측으로 더이상 움직일 수 없습니다.")
        else:
            line1[y][x] = "☆ "
            line1[y][x+1] = "★ "
            moved_star += 1
    elif move1 == "4":
        if x == 0:
            print("좌측으로 더이상 움직일 수 없습니다.")
        else:
            line1[y][x] = "☆ "
            line1[y][x-1] = "★ "
            moved_star += 1
    elif move1 == "8":
        if y == 0:
            print("위쪽으로 더이상 움직일 수 없습니다.")
        else:
            line1[y][x] = "☆ "
            line1[y-1][x] = "★ "
            moved_star += 1
    elif move1 == "2":
        if y == 4:
            print("아래쪽으로 더이상 움직일 수 없습니다.")
        else:
            line1[y][x] = "☆ "
            line1[y+1][x] = "★ "
            moved_star += 1
    elif move1 == "0":
        break
    else:
        print("올바른 방향을 입력해주세요.")
```
입력된 방향에 따라 조건을 만들어 이동시켜준다.
각 방향별로 x, y 인덱스를 +1또는 -1 해준 위치의 별을 검은 별로 바꾸어주고,
원래 위치의 별은 흰 별로 바꾸어주면 이동한 것 처럼 보이게 되고
"0" 입력 시 반복문에서 나가지도록 break를 설정한다.

또한 각 방향 끝에서는 더 이동이 되지 않도록 최소, 최대 인덱스에서는 이동불가 메세지를 출력한다.
그리고 이동 시 moved_star의 수가 1씩 증가하게 만들어 이동횟수를 측정한다.

### 4. 이동 횟수에 따른 결과 출력
```python
print(f"\n별의 이동 횟수: {moved_star}")
if moved_star >= 20:
    print("별은 뜨겁게 활활 타오릅니다!")
elif moved_star >= 15:
    print("별은 뜨거워졌습니다!")
elif moved_star >= 10:
    print("별에는 온기가 돕니다..!")
elif moved_star >= 5:
    print("별은 아직 차갑습니다...")
elif moved_star >= 3:
    print("별의 곳곳에 얼음이 보입니다...")
elif moved_star == 0:
    print("별에게는 아무 일도 일어나지 않았습니다...")
```
이동한 횟수에 따라 다른 상태를 출력하도록 조건문을 만들어 출력한다.
