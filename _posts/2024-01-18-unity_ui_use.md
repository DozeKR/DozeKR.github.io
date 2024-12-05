---
layout: single
title:  "[Unity] UI #04 How to use UI "
categories: Study
tag: [Unity, UI]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# 여러 해상도의 UI 설계

---
<p class="notice--info" style="font-size: 1rem !important;">
    <strong> - 참고 사항 -</strong>
    <br>
    <a herf="https://dozekr.github.io/study/unity_ui_canvas/"> 캔버스 스케일러(Canvas Scaler)</a>
    <br>
    <a herf="https://dozekr.github.io/study/unity_ui_layout/"> 앵커(Anchor)</a>
</p>

최신 게임과 어플은 아주 다양한 스크린 행상도를 지원해야 하는 경우가 많고, 특히 UI 레이아웃을 여러 해상도에 맞게 조정할 수 있어야 한다.

아래는 여러 해상도의 UI설계 방법에 대한 예시이다.


##  앵커를  사용하여 여러 종횡비 조정

![img](https://docs.unity3d.com/kr/2022.3/uploads/Main/UI_MultiResCenter.png)

UI 요소의 **앵커(Anchor)**가 중심일 경우 해상도가 가로 방향 종횡비로 변경되면 UI 요소가 스크린 사각형 안에 나타나지 않을 수 있다.

![img](https://docs.unity3d.com/kr/2022.3/uploads/Main/UI_MultiResCorners.png)

UI 요소를 스크린 위치에 해당하는 코너에 **앵커(Anchor)**를 설정하면 UI 요소가 스크린에 원하는 위치에 나타나게 할 수 있다.

![img](https://docs.unity3d.com/kr/2022.3/uploads/Main/UI_MultiResSizeChange.png)

스크린의  크기가 작아진 경우에도 앵커를 통해 원하는 위치에 나타난다. 하지만 오리지널 크기를 유지하기 떄문에 문제가 될 수 있다.

위와 같은 상황을 해결하기 위해 **Canvas Scaler**를 사용하여 비율을 조정할수 있다.

<br>

##  스크린 크기에 따른 스케일링

**캔버스 스케일러(Canvas Scaler)** 컴포넌트를 루트 **캔버스(Canvas)** 에 추가할 수 있다.

**캔버스 스케일러(Canvas Scaler)** 프로퍼티  **UI Scale Mode** 를 **Scale With Screen Size** 로 설정한다.

위 스케일 모드에서 레퍼런스로 사용할 해상도를 지정할 수 있다. 현재 스크린 해상도가 이 레퍼런스 해상도보다 더 크거나 작은 경우 캔버스의 스케일 팩터가 적절하게 설정되므로 모든 UI 요소가 스크린 해상도에 맞게 함께 확대 또는 축소된다.

**캔버스 스케일러(Canvas Scaler)** 프로퍼티 **Match**를 0.5로 설정하면 현재 너비를 레퍼런스 너비와 비교하고 현재 높이를 레퍼런스 높이와 비교한 후 이 두 비교값 사이에서 스케일 팩터를 선택한다.

위를 통해서 가로 세로 해상도에 대응할수 있게 된다.

적절한 **앵커(Anchor)**위치와 **캔버스 스케일러(Canvas Scaler)**를 조합하여 아래와 같이 여러해상도에 대응할 수 있다.

![img](https://docs.unity3d.com/kr/2022.3/uploads/Main/UI_MultiResAllResolutions.png)



<br>

# UI 요소를 콘텐츠 크기에 맞추기

---
<p class="notice--info" style="font-size: 1rem !important;">
    <strong> - 참고 사항 -</strong>
    <br>
    <a herf="https://dozekr.github.io/study/unity_ui_layout/"> 레이아웃(Layout)</a>
</p>

## 텍스트 크기에 맞추기

**텍스트(Text)** 컴포넌트가 있는 동일한 게임 오브젝트에 **Content Size Fitter** 컴포넌트를 추가한다.

가로 피트 및 세로 피트를 **Preferred**로 설정한다.

**피벗(Pivot)**의 위치의 반대방향으로 확장되는 것을 주의 해야한다.

<br>

## 하위 텍스트가 있는 UI 요소의 크기에 맞추기

**수평 레이아웃 그룹(Horizontal Layout Group)**과  **Content Size Fitter** 추가한다.

가로 피트와 세로 피트 중 하나 이상을 **Preferred**로 설정한다.

수평 레이아웃 그룹의 **패딩(Padding)** 프로퍼티를 사용하여 패딩을 추가하고 미세 조정할 수 있다.

<br>

## 레이아웃 그룹의 하위요소를 각각의 크기에 맞추기

**각 하위 요소마다 콘텐츠 크기 피터를 추가할 수는 없다**. 그 이유는 콘텐츠 크기 피터가 자체적인 사각 변환을 제어하려고 하지만 부모 레이아웃 그룹도 자식 사각 트랜스폼을 제어하려고 하기 때문에 충돌이 발생한다.

상위 요소의 레이아웃 그룹이 이미 각 하위 요소의 크기를 콘텐츠에 맞출 수 있다.

레이아웃 그룹에서 **하위 요소의 포스 확장 토글(Child Force Expand)을 비활성화**한다.

하위 요소도 레이아웃 그룹인 경우 Child Force Expand 비활성화해야 할 수도 있다.

자식이 더 이상 가변 너비로 확장되지 않는 경우 자식 정렬 설정을 사용하여 레이아웃 그룹에서 정렬을 지정할 수 있다.

추가 사용 공간을 채우기 위해 일부 자식을 확장하려면 확장하려는 하위 항목에 **Layout Element를 추가**하고 해당 레이아웃 요소에 Flexible Width 또는 Flexible Height 프로퍼티를 사용하면 쉽게 제어할 수 있다.

<br>
