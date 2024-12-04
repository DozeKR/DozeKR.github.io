---
layout: single
title:  "[Unity] UI #01 Canvas "
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



<br>


## 스크린 공간 - 카메라(Screen Space - Camera)

이 모드는 스크린공간-오버레이 랑 비슷하지만 캔버스가 특정 Camera(**Render Camera**)에서 주어진 거리(**Plane Distance**)만큼 앞쪽에 위치한다. 

카메라 설정이  UI의 모습에 영향을 준다.

아래의 예시 처럼 씬 안의 오브젝트 중 UI 평면보다 카메라에 가까운 모든 오브젝트는 UI 앞에 렌더링되고, UI가 가려진다.

![씬 오브젝트가 앞에 있는 카메라 모드 UI](https://docs.unity3d.com/kr/2022.3/uploads/Main/CanvasCamera.png)



<br>

## 월드 공간(World Space)

UI가 씬 안에 있는 평명 오브젝트인 것처럼 렌더링된다.  캔버스의 크기는 사각 트랜스폼을 사용하여 수동으로 설정 가능하고, UI 요소는 3D 배치에 기반하여 다른 오브젝트 앞 또는 뒤에 렌더링된다.

![씬 오브젝트를 가로지르는 월드 공간 UI](https://docs.unity3d.com/kr/2022.3/uploads/Main/CanvasWorldSpace.png)

<br>

# 캔버스 스케일러(Canvas Scaler)
---

Canvas Scaler 컴포넌트는 캔버스 내 UI 요소의 전체적인 스케일과 픽셀 밀도를 제어하는데 사용된다.

스케일은 글꼴 크기와 이미지 경계 등 **캔버스 아래의 모든 요소에 영향을 미친다.**

Canvas Scaler 와 Rect Transform의 앵커를 통해 여러 해상도의 대응할 수 있는 UI를 만들 수 있다. 자세한 내용은 [이 페이지](https://dozekr.github.io/study/unity_ui_use/)에 서술한다.

![CanvasScaler](/images/2024-01-15-unity_ui_canvas/CanvasScaler.PNG)



<br>

## 고정 픽셀 크기(Contant Pixel Size)

UI 요소가 화면 크기에 관계없이 동일한 픽셀 크기로 유지됩니다.

UI 요소의 포지션과 크기가 화면에서 픽셀로 지정된다.



| **프로퍼티**                  | **기능**                                                     |
| ----------------------------- | ------------------------------------------------------------ |
| **Scale Factor**              | 캔버스의 모든 UI 요소를 이 배율로 스케일한다.                |
| **Reference Pixels Per Unit** | 스프라이트에 이 ‘Pixels Per Unit’ 설정이 적용된 경우 스프라이트의 1픽셀이 UI의 유닛 하나에 해당된다. |



<br>

## 화면 크기에 따른 스케일(Scale With Screen Size)

화면 크기에 비례하여 UI 크기가 변한다.

지정된 레퍼런스 해상도의 픽셀 수에 따라 포지션과 크기를 지정할 수 있다.

현재 화면 해상도가 레퍼런스 해상도보다 큰 경우 캔버스의 해상도가 레퍼런스 해상도로 유지되지만 화면에 맞추어 더 크게 확대되고, 반대의 경우 더 작게 축소된다.



| **프로퍼티**                  | 기능                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| **Reference Resolution**      | UI 레이아웃에 적합한 해상도입니다. 화면 해상도가 크면 UI가 더 크게 스케일되고 작으면 UI가 더 작게 스케일된다. |
| **Screen Match Mode**         | 현재 해상도의 종횡비가 레퍼런스 해상도에 맞지 않는 경우 캔버스 영역을 스케일하는 데 사용되는 모드 |
| **Match Width or Height**     | 캔버스 영역의 너비 또는 높이를 레퍼런스로 사용하여 스케일하거나 그 사이로 스케일된다. |
| **Expand**                    | 캔버스 크기가 레퍼런스보다 더 작아지지 않도록 캔버스 영역을 수평 또는 수직으로 확장된다. |
| **Shrink**                    | 캔버스 크기가 레퍼런스보다 커지지 않도록 캔버스를 수평 또는 수직으로 자른다. |
| **Match**                     | 스케일링 레퍼런스로 너비 또는 높이를 사용할지, 아니면 둘 사이의 배합을 사용할지 결정한다. |
| **Reference Pixels Per Unit** | 스프라이트에 이 ‘Pixels Per Unit’ 설정이 적용된 경우 스프라이트의 1픽셀이 UI의 유닛 하나에 해당된다. |



<br>

## 고정 물리적 크기(Constant Physical Size)

화면 크기와 상관없이 동일한 물리적인 크기로 유지한다.

UI 요소의 포지션과 크기가 밀리미터, 포인트 또는 피카 등의 물리적인 단위로 지정된다.

이 모드를 사용하려면 기기의 화면 DPI 정확하게 알아야 한다.



| ***프로퍼티***                | ***기능***                                                   |
| ----------------------------- | ------------------------------------------------------------ |
| **Physical Unit**             | 포지션 및 크기를 지정하는 물리적 단위.                       |
| **Fallback Screen DPI**       | 화면 DPI를 알 수 없는 경우 가정되는 DPI.                     |
| **Default Sprite DPI**        | ‘Pixels Per Unit’ 설정이 ‘Reference Pixels Per Unit’ 설정과 일치하는 스프라이트에 사용할 인치당 픽셀(DPI)이다. |
| **Reference Pixels Per Unit** | 스프라이트에 ‘Pixels Per Unit’ 설정이 있는 경우 DPI는 ‘Default Sprite DPI’ 설정과 일치한다. |



<br>

# 캔버스 그룹(Canvas Group)
---

Canvas Group은  UI 요소 그룹 전체의 특정 측면을  한 곳에서 제어하기 위해 사용된다. 해당 오브젝트뿐만 아니라 하위 오브젝트에도 영향을 미친다.

![CanvasGroup](/images/2024-01-15-unity_ui_canvas/CanvasGroup.PNG)

| ***프로퍼티***           | ***기능***                                                   |
| ------------------------ | ------------------------------------------------------------ |
| **Alpha**                | 그룹에 있는 UI 요소의 불투명도를 나타낸다. 값은 01 사이이며 0이면 완전한 투명, 1이면 완전한 불투명이다. 모든 요소는 고유의 투명도를 보유하고 있기 때문에, 캔버스 그룹의 알파값과 개별 UI 요소의 알파값은 서로 증대된다. |
| **Interactable**         | 체크할 경우, 상호작용이 활성화된다.                          |
| **Block Raycasts**       | 체크할 경우, 캔버스에 부착된 그래픽 레이캐스터에서 레이캐스트 함수를 호출해야 한다. **Physics.Raycast**에는 적용되지 않는다. |
| **Ignore Parent Groups** | 체크할 경우, 상위에 있는 캔버스 그룹 컴포넌트의 설정의 영향을 받지 않고, 값을 본인의 값으로 치환한다. |

