---
layout: single
title:  "[YarnSpinner] #03 Yarn Scripts Configuration "
categories: Study
tag: [YarnSpinner]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# [YarnSpinner] #03 Yarn Scripts Configuration
## Node
노드는 대화를 넣을 수 있는 곳
파일에 링크하는 수만큼 노드를 가질 수 있음
노드는 이야기의 이부를 분리하고 더 긴 이야기와 분기를 관리하기 쉽게 만드는데 사용

각 노드에는 최소한 헤더와 본문이 있음
모든 노드에는 적어도 제목 헤더는 포함
제목은 노드 이름이고 본문에는 대화 내용을 담음

노드 제목을 사용하여 시작할 노드를 알려주기 때문에 노드 제목은 중요함
다른 노드로 점프하고 싶을 때 노드 제목을 사용

**노드 제목은 문자로 시작해야 하며 문자, 숫자 및 밑줄을 포함할 수 있음**
**노드 이름에는 ```.```을 포함할 수 없음**

```
title: Node_Title
---
Here are some lines!
Wow!
===
```
```---```는 본문의 시작점을 나나냄
```---```는 노드가 끝나느 위치를 나타냄


## Line
대화를 작성할 때 노드에 작성하는 텍스트는 거의 모든 행의 한 **Line** 으로 작성 
노드가 실행되면 각 라인을 한 번에 하나씩 실행
일반적으로 말하는 실체의 이름으로 시작
Line 시작 부분에 콜론```:``` 앞에 공백이 없는 문자 집합이 있을 경우, 이름으로 표시

```
안녕하세요(이름이 없는 캐릭터 대화도 가능)
P: 안녕하세요
P: 누구세요?
P: ... 
```



## Option
플레이어가 할 말을 결정하도록 하려면 Option 사용
플레이어에게 여러 잠재적 대사를 보여주고 플레이어가 하나를 선택할 수 있음
옵션은 ```->```로 표시

```
Q1 : 1 + 1 =
-> Player : 0
-> Player : 1
-> Player : 2
```

### Options and Lines
Option을 선택할 때 실행되는 고유한 Line을 가질 수 있음
```
Q1 : 1 + 1 =
-> Player : 0
  Q1 : false
-> Player : 1
  Q1 : false
-> Player : 2
  Q1 : true
```

### Nested Options
Option 안에 Option을 포함될 수 있음
```
Q1 : 1 + 1 =
-> Player : 1
  Q1 : false
  -> Player : 2
    Q1 : true
  -> Player : 3
    Q1 : false
-> Player : 2
  Q1 : true
```
