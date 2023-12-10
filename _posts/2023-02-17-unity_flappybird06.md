---
layout: single
title:  "[#U01] FlappyBirdLike #06"
categories: Coding
tag: [FlappyBird, Unity]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# [# U01] FlappyBirdLike 구현 #06

# 게임조건

**-게임 조건-**

1. 터치 및 클릭으로 캐릭터가 일정하게 떠오른다.

2. 천장 및 바닥에 캐릭터가 부딪히면 게임이 종료된다.

3. 장애물에 캐릭터가 부딪히면 게임이 종료된다.

4. 장애물은 일정 범위로 랜덤하게 생성된다.

5. 장애물 사이 공간을 지나갈 때 점수가 오른다.

   

# 사전 준비

![Prefap01](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-17-unity_flappybird06/Prefap01.png?raw=true)

이전 포스팅에서 미리 수정한 프리팹에 PointTrigger에 Is Trigger가 제대로 체크되어 있는지 확인합니다.



# 시작  

## 조건 05 구현하기



**조건05. 장애물 사이 공간을 지나갈 때 점수가 오른다.**



## 점수 표시 UI 생성

![UI01](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-17-unity_flappybird06/UI01.png?raw=true)

유니티에서 UI를 만들기 위해서는 먼저 Canvas를 생성해야 합니다.
하이어러키에 우클릭 > UI >> Canvas 를 생성하고 이름을 PointCanvas로 변경합니다.
PointCanvas를 클릭한 상태에서 우클릭 > UI > Lagacy > Text를 생성하고 이름을 Point로 변경합니다.



Point의 인스펙터 창을 자세히 보겠습니다.

![UI02](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-17-unity_flappybird06/UI02.png?raw=true)

**Rect Transform**은 화면 크기에 상관없이 **Anchor**로 기준점을 잡고 위치를 지정하기 때문에 항상 상대적인 비율로 원하는 위치에 배치할 수 있습니다.
Anchor의 Min, Max를 조정해서 Anchor의 비율을 정할 수 있습니다.

Text 컴포넌트는 저희가 아는 텍스트에 관련된 설정을 할 수 있습니다. 정렬, 굴게, 폰트크기, 폰트모양 등을 변경 가능합니다.




## 점수를 표시해주는(Point스크립트)

이제 Point오브젝트에 점수를 변경시켜줄 Point 스크립트를 생성하겠습니다.

**-Point 스크립트-**

```c#

using UnityEngine.UI;

public class Point : MonoBehaviour
{
    // 점수 변수
    public static int point = 0;  
    // 최고 점수 변수
    public static int bestpoint = 0;  

    void Start(){
        point = 0;
    }

    void Update(){
        GetComponent<Text>().text = point.ToString();
    }
}

```

먼저 UI 관련된 함수들을 가져오기 위해서 UnityEngine.UI를 추가합니다.
점수를 받는 변수를 생성하는데 점수는 자연수이기 때문에 int형으로 선언합니다.
여기서 점수를 올려주기 위해 다른 스크립트가 참조를 할 수 있게 하기위해 public으로 공통으로 변형하기 위해 static 을 사용한다.
마찬가지로 최고점수를 받기 위해 bestpoint도 똑같이 선언해줍니다.

Start함수에 게임이 시작할때마다 점수가 0으로 초기화 할 수 있게 만들어 줍니다.

실시간으로 점수는 바뀌기 때문에 Update 함수 안에 Text 컴포넌트를 받아와서 앞서 선언한 점수를 대입합니다. text는 스트링 형태이고 point는 인트형이기 때문에 .ToStirng으로 형변형을 시켜줍니다.




## 점수를 증가시켜주는(PointUP 스크립트)

![PointUP](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-17-unity_flappybird06/PointUP.png?raw=true)

만들어 놓은 프리팹에 PointTrigger에 스크립트를 추가하고 이름을 PointUp으로 바꿔줍니다.



**-PointUP 스크립트-**

```c#

public class PointUp : MonoBehaviour
{
    // 한번만 점수를 올리기 위한 변수
    int count = 0;
    private void OnTriggerExit2D(Collider2D other){
        if(count==0){
            Point.point++;
            count++;
        }
    }
}

```

OnTriggerExit함수가 작동하면 위에 선언한 point 변수가 상승하게 햇습니다.
트리거를 빠져나오면 발동해서 장애물을 넘을 때마다 1점씩 상승하겠지만, 혹시 모르는 예외사항이 있을 수 있기 때문에 count 인트형 변수를 선언해서 한번씩만 작동하게 했습니다.



## 게임 엔딩 씬 만들기

Scene은 여태 저희가 만들어놓은 하나의 화면을 말합니다. 씬을 통해서 저희는 게임오버 화면을 뛰울 생각입니다.

유니티 좌측 상단 File > NewScene > Basic 2D 로 씬을 만들고, 하이어러키 에서 씬을 선택한 상태에서 우클릭 > Save Scene as 저희가 만든 프로젝트에 GameOverScene으로 저장하겠습니다.

![NewScene](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-17-unity_flappybird06/NewScene.png?raw=true)



게임오버 씬을 아래 이미지와 같이 만들겠습니다.

![GameOverScene](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-17-unity_flappybird06/GameOverScene.png?raw=true)

캔버스, 패널, GameOver 텍스트, Point 텍스트, BestPoint 텍스트, Button 을 만들고, 취향에 맞게 앵커와 사이즈를 조정하여 꾸며줍니다. 

GamOverScene에 빈 오브젝트를 만들고 ReTry로 이름을 변경합니다.
ReTry 오브젝트에 Retry스크립트를 만듭니다.

**-Retry 스크립트-**

```c#

using UnityEngine.SceneManagement;

public class Retry : MonoBehaviour
{
    public void RetryGame(){
        SceneManager.LoadScene("PlayScene");
    }
}

```

씬을 변경할때는 UnityEngine.SceneManagement를 사용 해야합니다. SceneManager.LoadScene("원하는 씬의 이름")을 적어주면 원하는 씬으로 이동 가능합니다.




![Retry](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-17-unity_flappybird06/Retry.png?raw=true)

완성된 Retry스크립트를 캔버스에 만들어 놓은 RetryBtn의 OnClick 부분에 드래그 앤 드랍 해주고 RetryGame()함수를 실행할 수 있게 만들어 줍니다.




Point텍스트 오브젝트에는 EndPoint스크립트를 추가해줍니다.

**-EndPoint 스크립트-**

```c#

using UnityEngine.UI;

public class EndPoint : MonoBehaviour
{
 
    void Start(){
        GetComponent<Text>().text = "SCORE: " + Point.point.ToString();
    }

}

```

PlayScene에서 포인트와 다르게 게임이 종료됐을때 GameOverScene이 실행 됐을때만 보여주기 때문에 Stat함수에 text를 받아와 값을 넣어줍니다. 



BestPoint텍스트 오브젝트에는 BestPoint스크립트를 추가해줍니다.

**-BestPoint 스크립트-**

```c#

using UnityEngine.UI;

public class BestPoint : MonoBehaviour
{
   
    void Start(){
        GetComponent<Text>().text = "BEST: " + Point.bestpoint.ToString();
    }

}

```
여기에는 bestpoint의 값을 받아와줍니다.




마지막으로 기존 PlayerController스크립트를 수정하겠습니다.
**-PlayerController 스크립트-**

```c#

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class PlayerController : MonoBehaviour
{
    // Rigidbody변수 선언
    Rigidbody2D RB_Player;
    // 점프세기
    public float JumpPower = 5f;

    void Start(){
        RB_Player = GetComponent<Rigidbody2D>();
    }

    void Update(){
        if(Input.GetMouseButtonDown(0)){
            Debug.Log("jump");
            RB_Player.velocity = Vector2.up * JumpPower;
        }
    }

    // 플레이어가 다른 콜리전과 부딪혔을 때 실행
    private void OnCollisionEnter2D(Collision2D other){
        // 최고점수 저장
        if(Point.point > Point.bestpoint){
            Point.bestpoint = Point.point;
        }
        SceneManager.LoadScene("GameOverScene");
    }
}

```

플레이어가 다른 콜리전과 부딪혔을 경우에 실행하는 함수를 만들어줍니다.
부딪혔을 경우 point 와 bestpoint를 비교해서  bestpoint를 갱신해줍니다.
SceneManager.LoadScene("GameOverScene") 통해서 GameOverScene을 뛰워줍니다.



이제 마지막으로 테스트 화면입니다.

![test](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-17-unity_flappybird06/test.png?raw=true)



# 정리 

1. Rect Transform은 화면 크기에 상관없이 Anchor로 기준점을 잡고 위치를 지정하기 때문에 항상 상대적인 비율로 원하는 위치에 배치할 수 있다.
2. 씬을 변경할때는 UnityEngine.SceneManagement를 사용해야 한다. SceneManager.LoadScene("원하는 씬의 이름")을 통해 씬을 바꿀 수 있다.
3. public을 통해 외부에서 참조 가능한 변수를 만들 수 있다.