---
layout: single
title:  "[Unity] UI #05 UI Optimization"
categories: Study
tag: [Unity, UI]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# Unity UI 최적화

```
UI는 계속 갱신되기 때문에 Dirty Flag를 사용한다.
Dirty Flag는 개체나 컴포넌트의 속성이 변경됐음을 표시하여, 변화를 확인하는 방법이다.
계속 갱신되는 동안 연산을 할 수 없기 때문에 Dirty Flag 를 통해 변화가 있을 경우에만 연산을 하는 방식을 사용한다.
```
---

<br>

## 캔버스 분할

유니티 UI 는 캔버스 단위로 렌더링 하기 때문에 캔버스 안에 UI 요소가 변경될 경우 캔버스 전체를 Draw Call 을 하게 된다.

즉 하나의 캔버스에 모든 UI 요소를 넣게 되면 요소 중 하나가 변경되더라도 모든 UI 요소를 다시 그려줘야 한다.

위와 같은 상황을 피하기 위해서 동적/정적 캔버스로 나누어 주면 최적화에 효과적이다.

캔버스는 캔버스의 자식으로 들어갈 수 있기 때문에 정적인 캔버스 안에 동적인 캔버스를 자식으로 넣어 작업할 수 있다.

위와 같은 작업을 Nested Canvas 라고 한다.

<br>

## 그래픽 레이캐스터 제한 및 레이캐스트 타깃 비활성화

그래픽 레이캐스터는 사용자의 입력을 UI 이벤트로 변환하는 컴포넌트이다.

즉 상호작용이 필요하지 않은 UI에는 레이캐스트를 비활성화여 불필요한 연산을 줄일 수 있다.

<br>

## 보이지 않거나 사용하지 않는 UI는 숨기기

사용하지 않거나 보일 필요 없는 UI의 경우에도 Draw Call을 할 수 있다.

따라서 불필요한 연산을 하지 않기 위해 캔버스 컴포넌트 자체를 비활성화 하면 Draw Call을 하지 않기 때문에 캔버스 컴포넌트를 비활성화 해준다.

<br>

## UI 요소에서 최적의 애니메이터 사용

애니메이터는 값이 변경되지 않더라도 매 프레임마다 UI 요소를 Dirty 처리한다.

이를 해결하기 위해 UI 에서 애니메이션을 사용할때는 DoTween 을 활용한다.

