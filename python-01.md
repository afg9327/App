### 1번 문제

#### 문제
```
1. 멘토가 좋아하는 프링글스 스윗 마요를 만드는 인공지능 오븐을 개발하려고 한다. 적당한 양의 감자를 오븐에 넣으면 인공지능 오븐은 프링글스가 만들어지는 시각을 알려준다. 프링글스 만들기를 시작하는 시각과 오븐에 구워 완성을 하는데 필요하는 시간이 초 단위로 주어졌을 때, 프링글스 만들기가 끝나는 시각을 계산하는 프로그램을 작성하세요
입력
1. 첫째 줄에는 현재 시각이 나온다 ( (시) 0 <= A <= 23, (분) 0 <= B <= 59, (초) 0 <= C <= 59)
2. 둘째 줄에는 요리하는데 필요한 시간 (0<=D<=500000) 가 초 단위로 주어진다.
출력
첫째 줄에 종료되는 시각의 시, 분, 초를 공백을 사이에 두고 출력

```

1. 구태우님
```
startHours, startMin, startSec = map(int,input().split())
D = int(input())

startHours = (startHours * 3600 + startMin * 60 + startSec + D) // 3600 % 24
startMin = (startMin + (startSec + D) // 60) %60
startSec = (startSec + D) % 60

print(startHours, startMin, startSec)
```
너무 과한 숏코딩은 좋지 않지만 태우님의 코드는 가독성이 아주 좋습니다. 또 map 을 사용하신 것도 아주 좋았습니다. 또 태우님 코드는 60분 이상 60초 이상의 입력이 들어왔을 때에 대한 처리가 되어있습니다. GOOD! 하지만 23시도 입력받을 수 있으므로 이 부분을 추가적으로 고려할 수 있을 것 같습니다.
(혹시 map 이 뭔지 모르시는 분들은
[map이 뭘까?](https://blockdmask.tistory.com/531)
위의 링크를 참고하시길 바랍니다! 그래도 이해가 안되는 부분이 있으시다면 멘토에게 물어보세요! 직접 알려드리겠습니다!)
startHours, startMin, startSec 와 같이 변수명을 지을 때 프로그램에서 개발자의 의도를 명확히 해 줄 수 있도록 고민하신 것이 보여 좋았습니다. 다른 변수들도 통일성 있게 [ ex> 4번째 줄의 startHours(endHours), 3번째 줄의 D (processTime)] 이름을 고려하신다면 더 좋은 코드가 될 것 같습니다.
지금까지의 문제는 간단한 코딩이므로 변수명을 딱히 고려하지 않아도 이해할 수 있지만 미리 연습해두시는 걸 추천드립니다.
참고하실만한 링크를 첨부합니다.
[변수명은 어떻게 지어야 할까?](https://brunch.co.kr/@wapj2000/29)

**태우님 코드 기반으로 수정해 본 코드입니다.**
1. 24 시간 이상이 되었을때 처리
2. 변수명 수정
```
startHours, startMin, startSec = map(int,input().split())
processTime = int(input())

completeHours = (startHours * 3600 + startMin * 60 + startSec + processTime) // 3600 % 24
# 23 59 59 / 1 => 24 0 0 => 0 0 0
completeMin = (startMin + (startSec + processTime) // 60) %60
completeSec = (startSec + processTime) % 60

print(startHours, startMin, startSec)
```

2. 이용현님
```
hour , minu , seco = input().split()
hour = int(hour)
minu = int(minu)
seco = int(seco)
while True:
    bakeTime = int(input())
    if(0 <= bakeTime <= 500000):
        break
    else:
        print("값이 너무 큽니다, 500000 이하로 입력해주세요.")

allTime = hour*3600 + minu*60 + seco + bakeTime
allTime = allTime % 86400
hour, allTime = int(allTime/3600), int(allTime%3600)
minu, allTime = int(allTime/60), int(allTime%60)
seco = int(allTime)

print(hour, minu, seco)
```
예외처리가 굉장히 잘 되어있습니다! 코딩테스트에서 자주 볼 수 있는 예외처리는 아니지만 교수님들이 좋아하시는 훌륭한 과제에서 자주볼 수 있는 좋은 예외처리였습니다! 태우님도 마찬가지로 변수명을 고려해주신 것이 보여 좋았습니다. 또 하루가 지났을 때에 대해서도 처리하신 부분도 좋았습니다! 다만 나중에 다시 코드를 확인하였을 때 86400 이라는 수가 정확히 뭘 말하는거였더라? 헷갈릴 수 있을 것 같습니다. 파이썬에도 상수를 선언할 수 있습니다 (import constant1) 60 * 60 * 24 라는 주석을 추가한다면 더 좋을 것 같습니다. 또 input("프링글스가 굽는데 까지 걸리는 시간을 입력해 주세요 : ") 라고 작성하면 사용자 측면에서 조금 더 프로그램의 의도를 파악하기 좋을 것 같습니다 
피드백 드릴게 많이 없네요,,, 너무 훌륭합니다!

**용현님 코드 기반으로 수정해 본 코드입니다.**
```
# map 을 사용하여 코드를 줄일 수 있음
hour, minu, seco = map(int, input().split())

while True:
    bakeTime = int(input("프링글스가 굽는데 까지 걸리는 시간을 입력해 주세요 : "))
    # 아주 좋습니다!
    if(0 <= bakeTime <= 500000):
        break
    else:
        print("값이 너무 큽니다, 500000 이하로 입력해주세요.")

allTime = hour * 3600 + minu * 60 + seco + bakeTime
allTime = allTime % 86400 # GOOD!!
hour, allTime = allTime // 3600, allTime % 3600
minu, allTime = allTime // 60, allTime % 60 # int 를 사용하지 않고 // (몫), % (나머지) 를 사용하면 됨
seco = allTime

print(hour, minu, seco)
```

### 2번 문제

#### 문제
```
문제
팰린드롬이란 이효이, level, noon 과 같이 앞으로 읽을 때와 거꾸로 읽을 때 똑같은 단어이다. Danni, ruru 와 같은 것은 팰린드롬이 아니다.

입력
첫째 줄에 단어가 주어진다. 단어의 길이는 1보다 크거나 같고 100볻 작거나 같으며 알파벳 소문자로만 이루어져있다.

== 추가 ==
한글이나 대문자가 입력되어도 구분할 수 있는 팰린드롬 만들기

출력
첫째 줄에 팰린드롬이 주어진다면 1, 아니면 0을 출력한다.

```

1. 구태우 님
```
def palidrome(my_string):
    for i in range(len(my_string) // 2):
        if(my_string[i] != my_string[len(my_string) -1 -i]):
            return False
        return True
    
print(palidrome(input()))
```
문제 풀때 도움을 드렸던 부분이 많아 피드백 드릴것이 많지 않네요 ㅠㅠ 다만 이 부분에서도 변수명 관련해서 아쉬운 부분이 하나 보입니다! pelindrom 을 판별하는 함수이므로 isPelindrom 과 같이 함수명을 작성하였다면 팰린드롬인지 아닌지를 bool 을 return 하는 함수라는 것이 더 잘 와닿겠죠?

2. 이용현 님
```
str = input()

strCount = len(str) - 1
strCountHalf = int(len(str)/2)
loopCount = 0
trueFalse = 1

while(strCountHalf > 0):
    if(str[loopCount] != str[strCount]):
        trueFalse = 0
        break
    loopCount += 1
    strCount -= 1
    strCountHalf -= 1

print(trueFalse)
```
while 문과 for 문의 차이가 뭘까요?
while 문은 정확히 내가 얼만큼 순회를 해야할지 모를 때, for 문은 내가 정확히 몇번 순회해야 할지 알고 있을 때 주로 사용하게 됩니다. 위의 코드도 strCount 의 딱 반만큼 순회한다는 것을 알고 있으므로 for 문을 써도 좋을 것 같습니다. (이 문제에서는 크게 상관 없습니다! 잘하셨어요!) 이번에도 몫 연산을 사용하면 int 를 한번 더 쓰지 않아도( int(len(str)/2) => len // 2 ) 됩니다. 

**용현님 코드 기반으로 수정해 본 코드입니다.**
```
str = input()

strCount = len(str) - 1
strCountHalf = len(str) // 2
isPelindrom = 1
    
for step in range(strCountHalf):
    if(str[step] != str[strCount - step]):
        isPelindrom = 0
        break

print(isPelindrom)
```

3. 예지 님
```
word = input()
 
palindrome = 1
for i in range(len(word) // 2):
    if word[i] != word[-1 - i]:
        palindrome = 0
        break
 
print(palindrome)
```
파이썬에서 인덱싱 특징을 잘 이해하신 것이 보입니다. 코드가 짧고 가독성도 좋습니다! 변수명도 누가 보아도 잘 이해될 만큼 목적에 맞게 작성되었습니다. 아주 훌륭합니다! 함수로는 어떻게 구현할 수 있을까 고민해보는 것도 좋을 것 같습니다.
