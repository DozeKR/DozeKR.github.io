---
layout: single
title:  "[#U01] FlappyBirdLike #01"
categories: Coding
tag: [FlappyBird, Unity]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
---

# [# U01] FlappyBirdLike 구현 #01 

[FlappyBird리뷰](https://dozekr.github.io/gamereview/flappybird/){: .btn .btn--info}

**-게임 조건-**

1. 터치 및 클릭으로 캐릭터가 일정하게 떠오른다
2. 천장 및 바닥에 캐릭터가 부딪히면 게임이 종료된다.
3. 장애물에 캐릭터가 부딪히면 게임이 종료된다.
4. 장애물은 일정 범위로 랜덤하게 생성된다.
5. 장애물 사이 공간을 지나갈 때 점수가 오른다.


리뷰에서 파악한 게임조건을 유니티를 활용하여 쉽게 구현할 생각입니다.

# 시작

[Unity다운](https://store.unity.com/kr/download?gclid=Cj0KCQiAi8KfBhCuARIsADp-A551c5kKfOAVcE6jWVTW-V2mNXrpNT8yZgX3o9ZM3S9mlB3xIwn4U5YaAlMQEALw_wcB&gclsrc=aw.ds){: .btn .btn--info}


![newproject2D](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/newproject2D.png?raw=true)

에디터 버젼: 2021.3.18f1 에서 진행하겠습니다.
2D코어를 선택하고 프로젝트명을 바꾸고 프로젝트를 생성하겠습니다.

![firstscreen](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/firstscreen.png?raw=true)

프로젝트의 첫 화면입니다. 
좌측에 하이어러키 창에서 밑에 설명할 게임오브젝트를 생성 및 관리가 가능합니다.
하이어러키 창에서 게임오브젝트를 클릭할 경우 우측에 인스펙터창에서 게임오브젝트의 정보를 확인 가능합니다.
아래에 Project창에서 개발에 사용할 파일들을 관리 가능합니다. 옆에 콘솔창을 통해 에러등을 확인 가능합니다.

![changescreen](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/changescreen.png?raw=true)

화면 구성은 가각의 창을 드래그하여 커스텀이 가능합니다.

# 게임오브젝트(GameObject) 

![CreateGameObject](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/CreateGameObject.png?raw=true)

하이어러키 창에서 우클릭을 통해 게임오브젝트를 생성할 수 있습니다.
**게임오브젝트(GameObject)**는 겉모습을 보여주는 **포장지**의 역할을 합니다.

![CreateGameObject02](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/CreateGameObject02.PNG?raw=true)

하이어러키 창에서 우클릭 -> CreateEmpty 게임오브젝트를 생성하고,
하이어러키 창에서 우클릭 -> 2D Object -> Sprites -> Circle 게임오브젝트를 생성합니다.

# 컴포넌트(Component), 프로퍼티(Property)

![CreateGameObject02](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/CreateGameObject02.PNG?raw=true)

생성된 GameObject를 선택하고, 인스펙터창에서 선택한 게임오브젝트의 컴포넌트를 볼 수 있습니다.
인스펙터창에서 보이는 Transform은 GameObject의 컴포넌트입니다. 
Transform 컴포넌트는 게임오브젝트의 위치, 회전, 크기를 조절할 수 있습니다.

![CreateGameObject03](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/CreateGameObject03.PNG?raw=true)

Circle 게임오브젝트랑 비교하면 Sprite Renderer 컴포넌트의 유무의 차이를 알 수 있습니다.

![CreatComponent](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/CreatComponent.png?raw=true)

Add Component를 통해서 Sprite Renderer 컴포넌트를 추가하여 GameObject를 Circle과 똑같은 역할을 할 수 있게 만들 수 있습니다.  
즉 **컴포넌트(Component)**는 게임오브젝트가 어떤 기능을 할지 정하는 **내용물**의 역할을 합니다.
그리고 컴포넌트가 가지고 있는 **속성, 기능, 옵션**을 **프로퍼티(Property)**라고 합니다. 

# 간단한 조작

![CreateGameObject02](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/CreateGameObject02.PNG?raw=true)

인스펙터창에서 게임오브젝트의 이름이 변경 가능하고, 오브젝트를 식별해주는 태그, 아이콘을 설정 가능합니다.

Transform 컴포넌트에서 Position, Rotation, Scale의 값의 변경으로 게임오브젝트를 변화시킬 수 있습니다.

변경한 오브젝트를 Scene창에서 확인 가능합니다.

![w](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/w.PNG?raw=true)

단축키 (w)를 통해서 오브젝트의 위치 변경이 가능합니다.

![e](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/e.PNG?raw=true)

단축키 (e)를 통해서 오브젝트의  회전이 가능합니다.

![r](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird01/r.PNG?raw=true)

단축키 (r)을 통해서 오브젝트의 크기 변경이 가능합니다.

# 정리

**정리**

1. 게임오브젝트(GameObject)는 포장지
2. 컴포넌트(Component)는 내용물
3. 프로퍼티(Property)s는 컴포넌트의 속성, 기능, 옵션 같은 세부사항이다
