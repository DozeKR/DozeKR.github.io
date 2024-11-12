---
layout: single
title:  "[YarnSpinner] #04 Yarn Script Details"
categories: Study
tag: [YarnSpinner]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# [YarnSpinner] #04 Yarn Script Details
## Variables
변수는 숫자, String, bool 중 하나를 저장할 수 있음

### 변수 선언
```<<declare>>```문을 사용하여 변수 선언
```
/// 플레이어
<<declare $playerName = "Player">>
/// 골드
<<declare $gold = 0>>
/// 보스 클리어 체크
<<declare $isClearBoss = false>>
```
### 변수 설정
```<<set>>```문을 사용하여 변수에 정보 입력
```
<<set $playerName to "MAN">>
```
**변수 이름에는 공백이 포함되면 안되고, 첫 번째 문자는 문자여야 함**

## Flow Control

### 조건문
```<<if>>``` ```<<elseif>>``` ```<<else>>``` ```<<endif>>``` 를 활용하여 조건문을 표현할 수 있음
```
<<set $gold_amount to 5>>

Player: 이 빵을 살게요!

<<if $gold_amount < 10>>
    Baker: 돈이 턱 없이 부족하잖아! 당장 나가!
<<elseif $gold_amount < 15>>
    Baker: 돈이 조금 부족하군..
<<else>>
    Baker: 여기 있네
<<endif>>
```

### 조건부 옵션
```
Darklord: 도적이 되고 싶은 자는 나에게..
-> 로그로 전직 시켜 주지! <<if $Level > 10>>
-> 아직 레벨이 부족하군.
```

## Markup

## Commands

Yarn Spinner에 몇가지 내장 Command 및 사용자 지정 Command 활용 가능

Yarn Spinner에서 제공하는 2개의 내장 Command ```wait```, ```stop```이 있음

### wait
```wait```는 지정된 시간(초)동안 대화를 일시 중지한 후 다시 시작하는 Command
```
// 2초를 기다림
<<wait 2>>
```

### stop
```stop```은 노드에 끝에 도달한 것처럼 즉시 대화를 종료하는 Command
```
<<if $hp < 0>>
  You Die!
  <<stop>>
<<endif>>
```
### 커스텀 명령 
[Commands and Functions](https://docs.yarnspinner.dev/using-yarnspinner-with-unity/assets-and-localization) 문서 참조

## Functions
* **visited(string node_name)**
  * 노드를 한번이라도 방문한 적이 있음 true를 반환
* **visited_count(stirng node_name)**
  * 노드의 방문 횟수를 반환
* **random()**
  * 0과 1 사이의 난수를 반환
* **random_range(number a, number b)**
  * a와 b 사이의 난수를 반환
* **dice(number sides)**
  * 1과 sides 사이의 임의의 정수를 반환
* **round(number n)**
  * n 반올림
* **round_places(number n, number places)**
  * 소수점 n 이하로 반올림
* **floor(number n)**
  * n 내림
* **ceil(number n)**
  * n 올림

### 커스텀 기능 
[Commands and Functions](https://docs.yarnspinner.dev/using-yarnspinner-with-unity/assets-and-localization) 문서 참조

테스트 테스트

## Tags and Metadata
