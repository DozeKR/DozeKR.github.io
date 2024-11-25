---
layout: single
title:  "[#U01] FlappyBirdLike #05"
categories: Coding
tag: [FlappyBird, Unity]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
sidebar:
    nav: "counts"
---

# [# U01] FlappyBirdLike 구현 #05

# 게임조건

**-게임 조건-**

1. 터치 및 클릭으로 캐릭터가 일정하게 떠오른다.

2. 천장 및 바닥에 캐릭터가 부딪히면 게임이 종료된다.

3. 장애물에 캐릭터가 부딪히면 게임이 종료된다.

4. 장애물은 일정 범위로 랜덤하게 생성된다.

5. 장애물 사이 공간을 지나갈 때 점수가 오른다.

   

# 사전준비   
게임을 완성하기 위해 프리팹을 조금 수정하겠습니다.

![Prefap01]({{site.ur}}/images/2023-02-16-unity_flappybird05/Prefap01.png?raw=true)

**조건05. 장애물 사이 공간을 지나갈 때 점수가 오른다.**

위 조건을 만족시키기 위해서 빈프로젝트를 생성하고, PointTrigger로 이름을 변경합니다.  BoxCollider2D 컴포넌트를 Is Trigger 체크하고, 적절한 크기로 조정합니다.




# 시작

## 조건 04 구현하기



**조건04. 장애물은 일정 범위로 랜덤하게 생성된다.**




## 장애물 왼쪽으로 이동(Move 스크립트)
먼저 장애물을 왼쪽으로 이동하게 만들겠습니다.

![Prefap02]({{site.ur}}/images/2023-02-16-unity_flappybird05/Prefap02.png?raw=true)

위 이미지처럼 Spikes 프리팹 오브젝트에 스크립트를 생성하고 이름을 Move로 정하겠습니다.

**-Move 스크립트-**

```c#

public class Move : MonoBehaviour
{
    // 장애물이 나오는 시간 조정 변수
    public float speed = 1f;

    void Start(){
        
    }

    void Update(){
        // transform.position = transform컴포넌트의 position값
        // Vector3.left = (-1,0,0) 
        // 프레임 단위는 환경마다 다르기 때문에 Time.deltaTime을 활용한다.
        transform.position += Vector3.left * speed * Time.deltaTime;
        Debug.Log(transform.position);
    }

}

```

Move 스크립트를 위와 같이 작성합니다.
transform.position으로 해당 오브젝트의 transform 컴포넌트의 프로퍼티인 position값을 참조할 수 있습니다.
**transfrom.position의 값은 (x, y, z) 로 값이 반환**합니다.
**Vector3.left는 (-1, 0, 0)**의 값입니다. 이를 통해 Update() 안에 넣었기 때문에 매 프레임마다 값이 축적되어 좌측으로 이동하는 것처럼 보이게 됩니다.
하지만 여기서 중요한 문제가 발생하는데 **프레임은 게임을 플레이하는 환경마다 다르다**는 것입니다. 그래서 저희는 **Time.deltaTime**을 활용합니다.
**deltaTime = 지난 프레임이 끝날때까지의 시간** 입니다.

**-예시-**
* 30FPS는 1초에 30M
* 60FPS는 1초에 60M
  

위와 같이 프레임에 따라 크게 변화가 생깁니다. 
* 30FPS는 1초에 30M * 1/30(deltaTime)
* 60FPS는 1초에 60M * 1/60(deltaTime)
  

위와 같이 detaTime은 프레임이 다르더라도 1초에 같은 행동을 가능하게 합니다.

public float speed를 선언하고, Vector3.left * Time.deltaTime 식에 speed를 곱해주어 장애물의 이동속도를 조정할 수 있습니다.



![Prefap03]({{site.ur}}/images/2023-02-16-unity_flappybird05/Prefap03.png?raw=true)

테스트 결과입니다. 초마다 장애물의 position 값이 변하는 것을 확인할 수 있습니다.
이제 좌측으로 움직이는 장애물 Spikes 프리팹을 완성했습니다.




## 장애물 일정 범위 랜덤 생성(Spawner 스크립트)
완성한 Spikes 프리팹을 생성하는 제너레이터(스포너) 오브젝트를 만들겠습니다.

![SpawnPoint]({{site.ur}}/images/2023-02-16-unity_flappybird05/SpawnPoint.png?raw=true)

위 이미지처럼 빈오브젝트를 생성하고 SpwanPoint로 이름을 변경하고, Spawner라는 스크립트를 생성하여 컴포넌트로 추가하겠습니다.



**-Spawner 스크립트-**

```c#

public class Spawner : MonoBehaviour
{
    // Prefab을 받아올 변수 선언
    public GameObject spikes;
    // 리스폰 시간
    public float SpawnTime = 3f;
    // 타이머
    float timer = 0;
    
    void Start(){
        
    }

    void Update(){
        timer += Time.deltaTime;
        if(timer > SpawnTime){
            GameObject spawnspike = Instantiate(spikes);
            spawnspike.transform.position = new Vector3(5, Random.Range(-1.5f, 1.5f), 0);
            Destroy(spawnspike, 10.0f);

            timer = 0;
        }
    }
}

```

Move 스크립트에서 설명했듯이 프레임은 게임을 플레이하는 환경마다 다르기 떄문에 timer 변수와 SpawnTime 변수를 활용하여 타이머에 n프레임마다 1/n 을 축적하여 정해둔 SpawnTime보다 커질때만 작동할 수 있는 if 문을 만든다. 
Instantiate(spikes)를 통해 만들어 놓은 프리팹을 복제할 수 있다. 
여기서 우리는 새로 생성되는 오브젝트를 spawnspike 변수에 넣고, spawnspike.transform.position을 변경시켜주면서 일정 Y축 범위에 랜덤하게 생성하게 만들어준다.
랜덤하게 변수를 주는 Random.Range(x, y)를 활용하여 x ~ y의 범위에 랜덤하게 y축을 조정하여 생성한다.
마지막으로 계속 프리팹이 복제할 경우 메모리에 부담을 주기 때문에. Destroy(오브젝트, n)함수를 활용해 n초 후에 해당하는 오브젝트를 삭제시켜준다.



![mission04]({{site.ur}}/images/2023-02-16-unity_flappybird05/mission04.png?raw=true)

기존에 하이어러키에 있던 Spikes 오브젝트는 삭제시켜주고, SpawnPoint에 있는 Spawner 스크립트에 Spikes에 만들어 놓은 프리팹 Spikes를 드래그앤 드랍해주고, SpwanTime도 본인에 게임에 맞게 지정해줍니다.



![mission04_02]({{site.ur}}/images/2023-02-16-unity_flappybird05/mission04_02.png?raw=true)

테스트틀 통해 위 이미지처럼 나오는 것을 볼 수 있습니다. 장애물의 크기, 플레이어의 크기, 플레이어의 점프력, 장애물의 스폰시간,  장애물 사이의  공간, 장애물의 이동속도등을 조절하여 밸런스를 조정해 줍니다.



# 정리
1. transfrom 컴포넌트의 프로퍼티룰 Vector3(x, y, z) 형식으로 값을 받아올 수 있다.
2. 프레임은 게임을 플레이하는 환경마다 다르다. 그렇기에 Time.deltaTime을 곱해 초단위로 맞출 수 있다.
3. Instantiate()를 통해 만들어 놓은 프리팹을 복제할 수 있다.
4. Random.Range(x, y)를 통해 x ~ y 범위의 랜덤한 값을 받을 수 있다.