---
layout: single
title:  "[Unity] Draw Call & Batching"
categories: Study
tag: [Unity]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# 드로우콜 & 배칭

---

CPU가 GPU에게 "이거 그려" 하고 명령을 하는 것을 **드로우콜(DrawCall)** 이라 한다.

이렇게 드로우콜과 그래픽을 구성하는 상태의 데이터를 넘기는 것을 **배치(Batch)**라고한다. 

이 과정이 많으면 최적화의 문제가 생기는데 이것을 줄이는 방법을 **배칭(Batching)**이라고 한다.

<br>

## CPU와 GPU의 상호작용

CPU는 게임을 구성하고 잇는 오브젝트 콘텐츠를 데이터를 읽는 역할을 한다.

GPU는 위의 데이터를 기반으로 콘텐츠를 그리는 역할을 한다.

GPU가 작업중이라면, CPU는 GPU의 작업이 끝나는 것을 기다려야 한다.

위와 같은 사황으로 인해 커맨드패턴과 메시지 큐에 의한 비동기 방식을 활용한다.

CPU에서 GPU에 전달할 명령을 임시 공간에 저장하고, GPU가 여유가 생길 떄 명령을 하나씩 처리한다.

### 커맨드 버퍼(Command Buffer)

CPU의 각 스레드에서 GPU에 전달할 명령을 모듈화하여 커맨드 버퍼에 임시로 저장한다.

명령을 곧장 커맨드 큐에 전송하는 것은 데이터 동기화 문제로 최적화에 문제가 생길 수 있으므로, 명령들을 모아 버퍼단위로 전송하는 방식을 사용한다.

### 커맨드 큐 (Command Queue)

GPU에는 CPU와 GPU가 함께 공유하는 커맨드 큐가 존재한다.

GPU는 여유가 생길 때마다 큐에서 커맨드 버퍼를 차례로 명령을 처리한다.

<br>

## 드로우콜(Draw Call)

### 랜더 상태(Render Sates)

GPU가 랜더링을 수행하기 위해 필요한 정보(쉐이더, 메시, 텍스쳐 등등)

### 랜더 상태 변경(Render State Changes)

GPU에서 랜더링할 대상의 상태가 변경될 경우 수행된다.

### SetPass Call

쉐이더로 인한 랜더 상태 변경만을 의미한다.

쉐이더 내의 Pass, 마테리얼 자체의 변경, 쉐이더 내 파라미터들의 변경이 해당된다.

메시가 달라도 마테리얼이 같다면 SetPassCall은 1번만 발생한다.

### DP Call(Draw Primitive Call)

CPU가 GPU에 그리라는 명령을 직접적으로 호줄하는 것을 의미한다.

### 드로우콜(Draw Call)

CPU에서 GPU에 렌더링 명령을 전송하는 것을 의미한다.





<br>

## 배칭(Batching)