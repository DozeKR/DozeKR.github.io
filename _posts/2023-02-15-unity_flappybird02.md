---
layout: single
title:  "[#U01] FlappyBirdLike #02"
categories: Coding
tag: [FlappyBird, Unity]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# [# U01] FlappyBirdLike 구현 #02

# 사전준비
게임을 개발할 때 간단한 도형만으로 개발을 진행하면 완성도가 떨어져 보입니다.
그래서 본격적인 구현에 앞서서 사이트를 하나 소개시켜 드리겠습니다.

[opengameart](https://opengameart.org/){: .btn .btn--info}
이 사이트의 경우 저작권이 무려인 자료들을 다운 받을 수 있습니다.

[캐릭터](https://opengameart.org/art-search-advanced?keys=flappy&title=&field_art_tags_tid_op=or&field_art_tags_tid=&name=&field_art_type_tid%5B%5D=9&field_art_licenses_tid%5B%5D=4&sort_by=count&sort_order=DESC&items_per_page=24&Collection=){: .btn .btn--info}[배경](https://opengameart.org/content/seamless-hd-landscape-in-parts){: .btn .btn--info}
제가 다운받은 곳의 여기입니다.[장애물](https://opengameart.org/content/bevouliin-free-ingame-obstacles-cyclop-spikes){: .btn .btn--info}
제가 다운받은 곳의 여기입니다.

프로젝트에서 Assets을 선택하고, Assets 창에 우클릭 > Create > Folder를 생성합니다. 다운받은 자료를 드래그 앤 드랍해서 폴더에 넣습니다.

# 시작
## 카메라
![maincamera]({{site.ur}}/images/2023-02-15-unity_flappybird02/maincamera.png?raw=true)

위 그림과 같이 Main Camera 게임 오브젝트만 남기고 전에 생성한 오브젝트들을 지워줍니다.

Main Camera를 선택했을 때 Scene창에서 나오는 사각형의 영역이 실제 게임에서 보여주는 영역입니다.


## 화면조정
![gametab]({{site.ur}}/images/2023-02-15-unity_flappybird02/gametab02.png?raw=true)

우측의 Game 탭을 선택하면 실제 게임 화면을 확인 가능합니다.

저희가 구현하려는 FlappyBird는 휴대폰 사이즈의 게임이니 사이즈를 조정합니다.
Free Aspect > + > (Label = phone, Type = Aspect Ratio, 9:16)으로 만들겠습니다.



![gametab03]({{site.ur}}/images/2023-02-15-unity_flappybird02/gametab03.png?raw=true)

화면이 휴대폰 사이즈로 변경된 것을 확인할 수 있습니다.




## Player게임오브젝트 생성
![creategameobject]({{site.ur}}/images/2023-02-15-unity_flappybird02/creategameobject.png?raw=true)

하이어러키 창에서 우클릭 -> 2D Object -> Sprites -> Circle 게임오브젝트를 생성합니다.

이름: Player / Tag: Player / Layer: Default 로 설정합니다.
Transform 컴포넌트의 우측상단의 버튼을 눌러 Reset을 시켜주면 게임오브젝트가 원점에 위치합니다. Transform을 이용하여 원하는 위치, 크기, 방향을 설정합니다.

Sprite Renderer 컴포넌트는 그림을 보여주는 컴포넌트입니다.
 프로퍼티인 Sprite에 다운받은 캐릭터 이미지를 드래그 앤 드랍합니다.



## 콜라이더(Collider)

**콜라이더**는 **충돌 영역을 감지**하는 컴포넌트입니다.

![collider]({{site.ur}}/images/2023-02-15-unity_flappybird02/collider.png?raw=true)

Plater 게임오브젝트 선택 후 인스펙터창에서 
Add Component > col 검색 > Capsul Collider 2D 생성합니다.



![collider02]({{site.ur}}/images/2023-02-15-unity_flappybird02/collider02.png?raw=true)

Capsul Collider 2D 컴포넌트에서 Edit Collider 혹은 Offset과 Size를 조정하여 캐릭터에 맞게 초록색 충돌 영역을 조정합니다. 

Is Trigger를 체크하면 오브젝트가 충돌이 되지 않고, 다른 콜라이더를 통과하지만 지나갈 경우, 이벤트를 발생시킬수 있습니다. 



## 리지드바디(Rigibody)

**리지드바디**는 **물리엔진**을 사용할수 있게하는 컴포넌트입니다.



![rigidbody]({{site.ur}}/images/2023-02-15-unity_flappybird02/rigidbody.PNG?raw=true)

Rigidbody2D 컴포넌트를 Player게임오브젝트에 추가합니다.

| **프로퍼티**          | **기능**                                          |
|-------------------|-------------------------------------------------|
| **Body type**     | Dynamic, Kinematic, Static  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                   |
| **Dynamic**       | 물리 영향 + 움직임                                     |
| **Kinematic**     | 물리 여향 X + 움직임                                   |
| **Static**        | 물리 영향 X + 움직임 X                                 |
| **Mass**          | 질량                                              |
| **Linear Drag**   | 공기 저항                                           |
| **Angular Drag**  | 회전 저항                                           |
| **Gravity Scale** | 중력                                              |



저희는  Body Type : Dynamic / Collision Detection : Continuous 설정합니다.



# 정리
1. 콜라이더(Collider): 콜라이더는 충돌 영역을 감지하는 컴포넌트입니다.
2. 리지드바디(Rigibody): 리지드바디는 물리엔진을 사용할수 있게하는컴포넌트입니다.
