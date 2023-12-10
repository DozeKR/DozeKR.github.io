---
layout: single
title:  "[#U01] FlappyBirdLike #04"
categories: Coding
tag: [FlappyBird, Unity]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# [# U01] FlappyBirdLike 구현 #04

# 사전준비

![사전준비](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-16-unity_flappybird04/%EC%82%AC%EC%A0%84%EC%A4%80%EB%B9%84.png?raw=true)

위의 이미지처럼 천장과 바닥 오브젝트를 생성 해줍니다. 컴포넌트로 Box Collider 2D를 넣어줍니다.

# 시작
## OnCollison 함수
PlayerController 스크립트를 통해 알아보겠습니다.

```c#

void Update(){}

private void OnCollisionEnter2D (Collision2D collision)
{
    // 충돌이 발생할 때
    Debug.Log ("Enter");
}
private void OnCollisionStay2D (Collision2D collision)
{
    // 충돌이 진행중일 때
    Debug.Log ("Stay");
}
private void OnCollisionExit2D (Collision2D collision)
{
    // 충돌이 종료됐을 때
    Debug.Log ("Exit");
}

```
**-OnCollison함수 작동 방식-**
* OnCollisionEnter : 충돌이 발생할 떄 호출
* OnCollisionStay  : 충돌이 진행중일 때 호출
* OnCollisionExit  : 충돌이 종료됐을 때 호출

위와 같은 방식으로 작동합니다. Debug.Log를 활용해서 직접 확인 해보겠습니다.





![Collision](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-16-unity_flappybird04/Collision.png?raw=true)

바닥과 처음 부딪혔을때 "Enter"가 그 이후로 "Stay"가 호출돼는 것을 알 수 있습니다.



## OnTrigger 함수

```c#

private void OnTriggerEnter2D (Collider2D collision)
{
    // 트리거와 충돌이 발생할 때
    Debug.Log ("TEnter");
}
private void OnTriggerStay2D (Collider2D collision)
{
    // 트리거와 충돌이 진행중일 때
    Debug.Log ("TStay");
}
private void OnTriggerExit2D (Collider2D collision)
{
    // 트리거와 충돌이 끝났을 때
    Debug.Log ("TExit");
}

```

**-OnTrigger함수 작동 방식-**
* OnTriggerEnter : 트리거와 충돌이 발생할 떄 호출
* OnTriggerStay  : 트리거와 충돌이 진행중일 때 호출
* OnTriggerExit  : 트리거와 충돌이 종료됐을 때 호출



![Trigger](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-16-unity_flappybird04/Trigger.png?raw=true)

빈 오브젝트를 생성해 Trigger로 이름을 변경하고 Tag에 Trigger를 추가해줍니다. 그리고 태그를 Trigger로 바꿔주고 BoxCollider2D 컴포넌트를 추가하고 Is Trigger를 체크해줍니다.
트리거의 위치는 플레이어가 떨어질 위치에 조정해주고 테스트 합니다.



![Trigger02](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-16-unity_flappybird04/Trigger02.png?raw=true)

트리거와 충돌이 발생할때 "TEnter", 충돌중일 때 "TStay", 충돌이 종료됐을 때 "TExit"이 출력된걸 확인할 수 있습니다.




```c#

    private void OnTriggerExit2D (Collider2D collision)
    {
        // 트리거와 충돌이 끝났을 때
        Debug.Log ("TExit");
        if (collision.CompareTag("Trigger")){
             Debug.Log ("+1");        
        }
    }

```
Trigger 오브젝트를 만들때 붙여준 태그를 활용하여 if문을 활용할 수 있습니다.
**CompareTag()**는 괄호 안에 있는 Tag의 참/거짓을 반환합니다. 그렇기에 플레이어가 Trigger 태그가 달린 트리거를 지나가면 +1이 출력하게 코딩했습니다.



![Trigger03](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-16-unity_flappybird04/Trigger03.png?raw=true)

테스트 결과입니다. 트리거를 빠져나오면서 +1도 출력된 것을 확인할 수 있습니다.


# 게임조건

**-게임 조건-**

1. 터치 및 클릭으로 캐릭터가 일정하게 떠오른다.

2. 천장 및 바닥에 캐릭터가 부딪히면 게임이 종료된다.

3. 장애물에 캐릭터가 부딪히면 게임이 종료된다.

4. 장애물은 일정 범위로 랜덤하게 생성된다.

5. 장애물 사이 공간을 지나갈 때 점수가 오른다.

   

## 조건 01 구현하기
**조건01. 터치 및 클릭으로 캐릭터가 일정하게 떠오른다.**

위에서 작성한 PlayerController 스크립트를 처음상태로 만들고 진행하겠습니다.

**-PlayerController 스크립트-**

```c#

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
}

```
위와 같이 Rigidbody 변수와 JumpPower 변수를 선언합니다.
Start()에서 RB_Player을 초기화 시켜줍니다.
Update()에서 **Input.GetMouseButtonDown(0)**를 통해 마우스 클릭의 참/거짓을 반환받아 if문을 작성합니다. 
클릭했을 경우에 jump 메시지와 플레이어가 2D 벡터상에 위 * JumpPower로 가게 설정합니다.



![mission01](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-16-unity_flappybird04/mission01.png?raw=true)

실행해보면 마우스 클릭시 플레이어 오브젝트가 위로 올라가는 것과 "jump"가 출력되는 것을 확인할 수 있습니다.




# 정리
**-OnCollison함수 작동 방식-**
* OnCollisionEnter : 충돌이 발생할 떄 호출
* OnCollisionStay  : 충돌이 진행중일 때 호출
* OnCollisionExit  : 충돌이 종료됐을 때 호출

**-OnTrigger함수 작동 방식-**
* OnTriggerEnter : 트리거와 충돌이 발생할 떄 호출
* OnTriggerStay  : 트리거와 충돌이 진행중일 때 호출
* OnTriggerExit  : 트리거와 충돌이 종료됐을 때 호출