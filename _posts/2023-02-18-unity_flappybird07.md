---
layout: single
title:  "[#U01] FlappyBirdLike #07"
categories: Coding
tag: [FlappyBird, Unity]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# [# U01] FlappyBirdLike 구현 #07

전체적인 게임의 틀은 완성했습니다.
게임의 퀄리티를 조금 높여보겠습니다.



# 퀄리티 업

## 애니메이션 추가

게임의 생동감을 살려주기 위해 애니메이션을 추가해 보겠습니다.

Windows > Animation > Animation을 클릭합니다.

![animation01]({{site.ur}}/images/2023-02-18-unity_flappybird07/animation01.png?raw=true)

![animation02]({{site.ur}}/images/2023-02-18-unity_flappybird07/animation02.png?raw=true)

위의 이미지처럼 Animation 창이 뜨는 것을 확인할 수 있습니다. Animation탭을 끌어서 옮길 수 있습니다.



![animation03]({{site.ur}}/images/2023-02-18-unity_flappybird07/animation03.png?raw=true)

애니메이션을 만들 오브젝트인 Player을 선택하고 Animation 창에 Create를 클릭합니다. 밑의 이미지처럼 창이 뜨는 것을 확인할 수 있습니다.



![animation04]({{site.ur}}/images/2023-02-18-unity_flappybird07/animation04.png?raw=true)

애니메이션을 만들 이미지를 그림가 같은 위치에 드래그 앤 드랍하여 애니메이션을 만들 수 있습니다. Player : Sprite 좌측 ▼ 를 클릭하면 위 이미지와 같이 화면을 볼 수 있습니다.



![animation05]({{site.ur}}/images/2023-02-18-unity_flappybird07/animation05.png?raw=true)

이미지의 순서를 더 추가하고 시간을 조정하여 만들어 더 자연스러운 애니메이션을 만들어 줍니다.



![background]({{site.ur}}/images/2023-02-18-unity_flappybird07/background.png?raw=true)

다운받은 배경이미지를 Scene에 드래그 앤 드랍하여 오브젝트를 만들어 줍니다. 



![Layer]({{site.ur}}/images/2023-02-18-unity_flappybird07/Layer.png?raw=true)

게임을 실행했을 때 플레이어가 사라지거나 깜빡이는 경우가 발생할 수 있습니다.  이것은 Order in Layer을 통해 수정할 수 있습니다. **Order in Layer는 보여줄 우선순위를 정해줍니다.** 숫자가 크면 클수록 우선순위가 높아집니다.



![floor]({{site.ur}}/images/2023-02-18-unity_flappybird07/floor.png?raw=true)

플레이어가 움직이는 것처럼 보이기 위해 바닥을 기존의 Spike를 통해 조금 변경했습니다. Draw Mode를 Tiled로 바꾸면 타일처럼 이미지를 그릴 수 있습니다. 이를 통해 바닥을 각진 벽돌처럼 표현했습니다. 그리고 포인트 부분의 텍스트 색을 잘 보일 수 있는 색으로 변경했습니다.



![animation06]({{site.ur}}/images/2023-02-18-unity_flappybird07/animation06.png?raw=true)

Floor을 선택하고 애니메이션을 추가합니다. 애니메이션을 빨간색원 버튼을 통해서 처음위치에서 원하는 초를 클릭하고 우측으로 이동하여 빨간색원 버튼을 다시 눌러줍니다.



![animation07]({{site.ur}}/images/2023-02-18-unity_flappybird07/animation07.png?raw=true)

조금 어려울 수 있지만 위의 이미지처럼 자연스럽게 초를 찍어 만들어 줍니다. 이후에 좀더 자연스럽게 연출하기 위해 드래그하고 우클릭 > Both Tnagents > Linear로 설정합니다.



## 효과음 추가

[효과음연구소](https://soundeffect-lab.info/){: .btn .btn--info}[변환사이트](https://convertio.co/kr/mp3-wav/){: .btn .btn--info}

위 사이트는 일본의 저작권 무료 효과음 사이트입니다. 유용하게 활용하기 바랍니다.
원하는 음원을 다운 받으면 유니티에 사용하기 위해서 wav형식으로 변환해야 합니다. 



![sound01]({{site.ur}}/images/2023-02-18-unity_flappybird07/sound01.png?raw=true)

플레이어에 Audio Source 컴포넌트를 추가합니다. Play On Awake를 꺼주고 변환한 음원 파일을 AudioClip에 넣어줍니다.
터치 및 클릭 시 플레이어가 날아오를 때 효과음이 나오게 설정하기 위해 PlayerController스크립트를 조금 수정하겠습니다.


**-PlayerController 스크립트-**

```c#

void Update(){
    if(Input.GetMouseButtonDown(0)){
        GetComponent<AudioSource>().Play();
        RB_Player.velocity = Vector2.up * JumpPower;
    }
}

```
플레이어 컨트롤 스크립트에 Update() 안에 클릭시 점프를 하던 조건문 안에 AudioSource 컴포넌트를 받아와서 Play함수를 실행하게 만들어 줍니다.



## 안드로이드 환경 테스트

먼저 안드로이드 스마트폰을 USB로 연결하고 설정 > 휴대전화 정보 >  소프트웨어 정보 >  비들번호를 여러번 터치 > 개발자 모드 켜기 > 설정 > 개발자 옵션 > USB 디버깅을 켜줍니다.

다시 유니티로 돌아와서 File > Build Settings를 켜줍니다.

![build]({{site.ur}}/images/2023-02-18-unity_flappybird07/build.png?raw=true)

처음 키시는 분들은 Windows, Mac, Linux로 설정돼 있을겁니다. 이것을 Android로 바꿔주고 switch 해줍니다. 이후에 Build And Run을 실행합니다.



![test01]({{site.ur}}/images/2023-02-18-unity_flappybird07/test01.png?raw=true)

핸드폰에 화면이 실행된 것을 확인할 수 있습니다. 하지만 텍스트에 조금 문제가 있습니다. 이것을 수정하겠습니다.



![fontchange01]({{site.ur}}/images/2023-02-18-unity_flappybird07/fontchange01.png?raw=true)

PointCanvas에 들어가서 CanvasScaler컴포넌트에 UI Scale Mode를 Scale Width Screen Size로 변경하고 폰 기종에 맞는 비율을 적어줍니다. 저는 1440 3040으로 설정했습니다.



![fontchange02]({{site.ur}}/images/2023-02-18-unity_flappybird07/fontchange02.png?raw=true)

그리고 Point 오브젝트에 들어가서  BestFit을 체크해주고 사이즈를 적절하게 수정합니다.



![fontchange03]({{site.ur}}/images/2023-02-18-unity_flappybird07/fontchange03.png?raw=true)

게임오버씬도 위와 같은 방법으로 수정합니다.



![test02]({{site.ur}}/images/2023-02-18-unity_flappybird07/test02.png?raw=true)

다시 Build And Run을 실행한 결과입니다 원하는 사이즈의 폰트가 나온것을 확인할 수 있습니다.



# 정리

1. 애니메이션은 Windows > Animation > Animation로 Animation 창을 만들어 오브젝트를 선택한 상태에서 Create하여 만들 수 있다.
2. Audio Source컴포넌트를 통해 음악을 넣을 수 있다.
3. File > Build Settings통해 빌드를 설정하고 만들 수 있다.