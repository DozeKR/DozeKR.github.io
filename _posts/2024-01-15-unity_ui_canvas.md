---
layout: single
title:  "[UnityUI] #01 Canvas "
categories: Study
tag: [Unity, UI]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# 캔버스(Canvas)
----

유니티의 모든 UI요소는 Canvas 안에 위치해야 한다.

즉 모든 UI요소는 반드시 어떤 캔버스의 자식이어야 한다.

<br>

# UI 요소 그리기 순서
---

캔버스 내에 UI 요소는 계층 구조에 나타나는 것과 동일 순서로 그려진다.

계층 구조의 첫 번째 UI요소가 처음으로 그려지고, 두 번째  UI요소가 다음 순서로 그려진다.

만약 두 UI요소가 겹쳐져 있다면 나중에 그려진 것이 위에 나타난다.

![DrawingOrder]({{site.url}}/images/2024-01-15-unity_ui_canvas/DrawingOrder.PNG)

![DrawingOrder](/images/2024-01-15-unity_ui_canvas/DrawingOrder-1732784445108-3.PNG)

<br>

# 프로퍼티
---

| **프로퍼티**                             | **기능**                                                                         |
|------------------------------------------|----------------------------------------------------------------------------------|
| **Render Mode**                          | UI가 스크린으로 렌더링 되거나 3D 공백에서 오브젝트로 렌더링되는 방법을 나타낸다. |
| **Pixel Perfect<br>(Screen Space)**     | 체크 할 경우, 안티앨리어싱 없이 UI를 렌더링 한다.                                |
| **Render Camera<br>(Camera mode)**     | UI가 렌더링될 카메라이다.                                                        |
| **Plane Distance<br>(Camera mode)**    | 카메라 앞으로부터 UI 평면이 위치할 곳 까지의 거리를 나타낸다.                    |
| **Event Camera<br>(World Space mode)** | UI 이벤트를 처리하는 데 사용될 카메라이다                                        |

## 안티앨리어싱


![img](https://docs.unity3d.com/kr/2018.4/uploads/Main/PostProcessing-Antialiasing-0.jpg)



안티앨리어싱을 사용하면 픽셀 주변의 블러 처리를 통해 부드럽게 보이게 할 수 있다.

<br>

# 렌더 모드(Render Mode)
---

캔버스에는 스크린 공간 또는 월드 공간에 렌더링하도록 하기 위해 사용되는 렌더 모드 설정이 있다.

캔버스에는 스크린 공간 또는 월드 공간에 렌더링하도록 하기 위해 사용되는 렌더 모드 설정이 있다.

## 스크린 공간 - 오버레이(Screen Space - Overlay)

이 모드는 UI 요소가 화면에서 씬의 위에 렌더링 된다. 스크린 크기가 조절되거나 해상도가 변경되면 캔버스는 여기에 맞춰 자동으로 크기를 변경한다.

![씬 오브젝트 위에 렌더링 된 오버레이 UI](https://docs.unity3d.com/kr/2022.3/uploads/Main/CanvasOverlay.png)


## 스크린 공간 - 카메라(Screen Space - Camera)

이 모드는 스크린공간-오버레이 랑 비슷하지만 캔버스가 특정 Camera(**Render Camera**)에서 주어진 거리(**Plane Distance**)만큼 앞쪽에 위치한다. 

카메라 설정이  UI의 모습에 영향을 준다.

아래의 예시 처럼 씬 안의 오브젝트 중 UI 평면보다 카메라에 가까운 모든 오브젝트는 UI 앞에 렌더링되고, UI가 가려진다.

![씬 오브젝트가 앞에 있는 카메라 모드 UI](https://docs.unity3d.com/kr/2022.3/uploads/Main/CanvasCamera.png)

## 월드 공간(World Space)

UI가 씬 안에 있는 평명 오브젝트인 것처럼 렌더링된다.  캔버스의 크기는 사각 트랜스폼을 사용하여 수동으로 설정 가능하고, UI 요소는 3D 배치에 기반하여 다른 오브젝트 앞 또는 뒤에 렌더링된다.

![씬 오브젝트를 가로지르는 월드 공간 UI](https://docs.unity3d.com/kr/2022.3/uploads/Main/CanvasWorldSpace.png)

<br>

# 캔버스 스케일러
---


<br>

# 캔버스 그룹
---
