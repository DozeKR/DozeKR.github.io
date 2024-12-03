---
layout: single
title:  "[Unity] UI #03 Component "
categories: Study
tag: [Unity, UI]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# 비주얼 컴포넌트(Visual Component)

---

## 텍스트(Text)

![image-20241203182227954](/images/2024-01-17-unity_ui_component/image-20241203182227954.png)

| **프로퍼티**                 | **기능**                                                     |
| :--------------------------- | :----------------------------------------------------------- |
| **Text**                     | 컨트롤에 의해 표시되는 텍스트                                |
| **문자**                     |                                                              |
| \- &ensp;Font                | 텍스트 표시에 사용되는 [폰트](https://docs.unity3d.com/kr/2022.3/Manual/class-Font.html) |
| \- &ensp;Font Style          | 텍스트에 적용되는 스타일입니다. *Normal*, *Bold*, *Italic*, *Bold And Italic* 옵션이 있다. |
| \- &ensp;Font Size           | 표시된 텍스트의 크기                                         |
| \- &ensp;Line Spacing        | 텍스트 행 간격                                               |
| \- &ensp;Rich Text           | 텍스트 마크업 요소를 [리치 텍스트](https://docs.unity3d.com/kr/2022.3/Manual/StyledText.html) 스타일링으로 간주할지 여부 |
| **문단**                     |                                                              |
| \- &ensp;Alignment           | 텍스트의 수평 및 수직 정렬입니다.                            |
| \- &ensp;Align by Geometry   | 글리프 지오메트리 범위를 사용해 글리프 메트릭이 아닌 수평 정렬을 수행합니다. |
| \- &ensp;Horizontal Overflow | 텍스트가 너무 넓어 사각형에 들어가지 않는 경우 사용하는 방법이다. Wrap(다음 행으로 내려 쓰기) 과 Overflow(가로 범위 넘어가도록 허용) 옵션이 있다 |
| \- &ensp;Vertical Overflow   | 래핑된 텍스트가 너무 길어 사각형에 들어가지 않는 경우 사용하는 방법입니다. Truncate(넘어간 글자는 잘라내어 미표시) 과 Overflow(세로 범위를 넘가도록 허용) 옵션이 있습니다. |
| \- &ensp;Best Fit            | Unity가 크기 프로퍼티를 무시하고 텍스트를 컨트롤 사각형에 맞출지 여부 |
|                              |                                                              |
| \- &ensp;Color               | 텍스트 렌더링에 사용되는 컬러                                |
| \- &ensp;Material            | 텍스트 렌더링에 사용되는 [머티리얼](https://docs.unity3d.com/kr/2022.3/Manual/class-Material.html) |

**텍스트(Text)** 는사용자에게 상호작용이 되지 않는 텍스트를 표시한다.

위의 유니티에서 지원하는 Text 컴포넌트는 시각적 품질이 매우 좋지 않아서 텍스트가 아닌 **Text Mesh Pro** 를 사용한다.

<br>

### Text Mesh Pro

---

![image-20241203182432275](/images/2024-01-17-unity_ui_component/image-20241203182432275.png)

| **프로퍼티**              | **기능**                                                     |
| ------------------------- | ------------------------------------------------------------ |
| **Text Input**            | 화면에 출력될 텍스트를 타이핑하는 공간<br />여러 줄을 입력할 때 Enter로 줄 바꿈, 서식 있는 텍스트(리치 텍스트)적용 가능 |
| **Text Style**            | 텍스트의 크기, 색상 등이 적용된 텍스트 스타일                |
| **Main Settings**         |                                                              |
| \- &ensp;Font Asset       | 텍스트 렌더링에 사용되는 폰트 에셋 (폰트 에셋에 설정된 글자만 정상 출력) |
| \- &ensp;Material Preset  | 텍스트에 적용되는 머터리얼(셰이더) 외곽선과 같은 추가 효과 적용 |
| \- &ensp; Font Style      | 텍스트에 굵게, 기울이기 등의 효과 적용                       |
| \- &ensp; Font Size       | 텍스트 크기                                                  |
| \- &ensp; Auto Size       | RectTransform과 텍스트 길이를 고려해 동적으로 폰트 크기 변화 여부 |
| \- &ensp; Vertex Color    | 폰트 색상                                                    |
| \- &ensp; Color Gradient  | 색상 그라데이션 설정                                         |
| \- &ensp; Spacing Options | 문자, 문장, 줄 간격 등 조절                                  |
| \- &ensp; Alignment       | 텍스트 정렬                                                  |
| \- &ensp; Wrapping        | 텍스트가 RectTransform을 넘어갈경우 다음 행으로 내려 쓸지 여부 |
| \- &ensp; Overflow        | 텍스트가 RectTransform을 넘어갈경우 처리하는 방법 선택       |
| **Extra Settings**        |                                                              |
|                           | 외곽 영역 간격, 리치 텍스트 사용 여부, 상호작용 여부 등을 설정 |

**TextMesh Pro**를 사용한다면 시각적 품질을 크게 개선할 뿐만 아니라 텍스트 스타일 지정 부문에서 뛰어난 유연성을 제공한다.

[Text Mesh Pro 참고 영상1](https://youtu.be/y8-GWxmosxo) 

[Text Mesh Pro 참고 영상2](https://youtu.be/y8-GWxmosxo)

<br>

## 이미지(Image)

![image-20241203190853370](/images/2024-01-17-unity_ui_component/image-20241203190853370.png)

| **프로퍼티**        | **기능**                                                     |
| :------------------ | :----------------------------------------------------------- |
| **Source Image**    | 표시할 이미지를 나타내는 텍스처 ([스프라이트](https://docs.unity3d.com/kr/2022.3/Manual/class-TextureImporter.html) 형식으로 가져와야 한다) |
| **Color**           | 이미지에 적용할 컬러                                         |
| **Material**        | 이미지 렌더링에 사용되는 [머티리얼](https://docs.unity3d.com/kr/2022.3/Manual/class-Material.html) |
| **Raycast Target**  | **Raycast Target** 을 활성화하면 Unity가 이미지를 레이캐스팅 대상으로 간주한다. |
| **Image Type**      |                                                              |
| \- &ensp;Simple     | 전체 스프라이트를 균일하게 스케일                            |
| \- &ensp;Sliced     | 3x3 스프라이트 분할을 활용하여 크기를 조절할 때 모서리 부분은 왜곡하지 않고 중심 부분만이 늘어나도록 한다. |
| \- &ensp;Tiled      | 슬라이스와 유사하나 중심 부분을 늘리는 것이 아니라 타일링(반복)한다. |
| \- &ensp;Filled     | 심플 옵션의 경우와 동일한 메서드로 스프라이트를 보여주되 원점으로부터 지정 방향, 방법, 양만큼 스프라이트를 채운다. |
| **Preserve Aspect** | 이미지가 기존 크기를 유지하도록 만든다.                      |
| **Set Native Size** | 이미지 박스의 크기를 텍스처의 원래 픽셀 크기로 설정한다.     |

**Image** 는사용자에게 상호작용하지 않는 이미지를 표시한다.

<br>

## 로우 이미지(Raw Image)

![image-20241203191723511](/images/2024-01-17-unity_ui_component/image-20241203191723511.png)

| **프로퍼티**       | **기능**                                                     |
| :----------------- | :----------------------------------------------------------- |
| **Texture**        | 표시할 이미지를 나타내는 텍스처                              |
| **Color**          | 이미지에 적용할 컬러                                         |
| **Material**       | 이미지 렌더링에 사용되는 [머티리얼](https://docs.unity3d.com/kr/2022.3/Manual/class-Material.html). |
| **Raycast Target** | **Raycast Target** 을 활성화하면 Unity가 이미지를 레이캐스팅 대상으로 간주한다. |
| **UV Rectangle**   | 컨트롤 사각형 안 이미지의 오프셋과 크기를 0.0 ~1.0 범위 정규화된 좌표로 나타낸 값. 이미지 모서리를 늘려 UV 사각형 주변 공간을 채운다. |

**Raw Image** 는 사용자에게 상호작용하지 않는 이미지를 표시한다

**Image** 의경우 텍스처가 스프라이트여야 하는 반면, **Raw Image**는 모든 텍스처를 사용할 수 있다.

<br>

## 마스크(Mask)

![image-20241203192131057](/images/2024-01-17-unity_ui_component/image-20241203192131057.png)

**Mask**는 눈에 보이는 UI 컨트롤이라기보다는 하위 요소의 외형을 수정하는 방식이다. 마스크는 하위 요소를 상위의 형태대로 제약(즉 “마스킹”)한다. 따라서 하위가 상위보다 클 경우 상위에 들어맞는 하위의 일부분만이 보일 수 있게 된다.

<br>

# 상호작용 컴포너트(Interaction Component)

---


<br>

## 선택 가능 베이스 클래스(Selectable)

<br>

## 버튼(Button)



<br>

## 토글(Toggle)


<br>

## 토글 그룹(Toggle Group)



<br>

## 슬라이더



<br>

## 스크롤바



<br>

## 드롭다운



<br>

## 입력필드



<br>

## 스크롤 사각 영역



<br>