---
layout: single
title:  "[#U01] FlappyBirdLike #03"
categories: Coding
tag: [FlappyBird, Unity]
toc: true 
toc_sticky: true 
toc_label: 목차    
author_profile: false
---

# [# U01] FlappyBirdLike 구현 #03

게임 조건을 다시 확인하겠습니다. 

**-게임 조건-**

1. 터치 및 클릭으로 캐릭터가 일정하게 떠오른다
2. 천장 및 바닥에 캐릭터가 부딪히면 게임이 종료된다.
3. 장애물에 캐릭터가 부딪히면 게임이 종료된다.
4. 장애물은 일정 범위로 랜덤하게 생성된다.
5. 장애물 사이 공간을 지나갈 때 점수가 오른다.

오늘은 **4번 조건인 장애물은 일정 범위로 랜덤하게 생성된다.** 부분을 준비하겠습니다.

# 시작
## 프리팹(Prefab)
**프리팹**은 슈팅 게임에 탄막이나 저희가 구현하려는 FlappyBird의 장애물같이 반복적으로 나오는 게임오브젝트를 **효율적인 재상용**을 위해 사용하는 것입니다.

프리팹을 만들기 위해서는 완성된 게임오브젝트가 필요한데 먼저 장애물 오브젝트를 만들겠습니다.

![spikes](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird03/spikes.PNG?raw=true)

빈게임오브젝트를 생성하고 Spikes로 이름을 변경합니다. Spikes에 마우스를 둔 상태에서 우클릭을 통해 sprites 오브젝트를 생성하면 Spikes부모로 하는 자식 오브젝트를 만들 수 있습니다. 자식 오브젝트 top, bottom 두개를 만들겠습니다.

 ![spikes02](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird03/spikes02.png?raw=true)

top, bottom 오브젝트에 다운받은 장애물 이미지를 sprite에 드래그 앤 드랍 하고 크기와 위치를 조절하여 장애물처럼 만듭니다. 그리고 모양에 맞게 콜라이더를 추가해줍니다. 저는 Caspsul Collider 2D를 넣었습니다.



![spikes03](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird03/spikes03.PNG?raw=true)

Spikes 부모 오브젝트에 Rigidbody 2D 를 추가하고, 물리 영향은 받지 않지만 스크립트를 통해서 움직일 수 있는 Kinematic으로 설정하겠습니다. 

여기에서 부모-자식간의 리지드바디로 여러가지 연출을 할 수 있는데 나중에 밑에서 따로 이야기 하겠습니다.

장애물 오브젝트는 이제 완성했습니다.



![prefabs01](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird03/prefabs01.PNG?raw=true)

위 처럼 먼저 프로젝트 창에서 Prefabs 폴더를 만들겠습니다. **폴더명인 Prefabs 는 미리 정의된 폴더이름이라 스팰링이 틀리지 않게 조심해야 합니다.**



![prefabs02](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird03/prefabs02.png?raw=true)

Prefabs 폴더에 완성한 Spikes 오브젝트를 드래그 앤 드랍 해줍니다. 하이어러키 창에서 Spikes 오브젝트가 파란색으로 변하면 프피팹으로 변한겁니다.



![prefabs03](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird03/prefabs03.png?raw=true)

위 이미지에서 변한 것이 보이나요? 실수로 프리팹을 삭제하면 오브젝트가 붉은색으로 변한 것을 볼 수 있습니다. 이 때는 붉은색으로 변한 오브젝트를 우클릭 > Prefab > Unpack 하면 기본 오브젝트로 만들 수 있습니다. 확인 했으면 다시 Spikes 오브젝트를 프리팹으로 만들겠습니다.

이것으로 프리팹을 완성했습니다.



## (상속)부모-자식 관계
프로그래밍을 하면서 부조-자식 관계 즉 상속은 한 번쯤 들어봤을 겁니다.
한 마디로 부모의 재능을 자식이 물려받는 개념입니다. 

여기서 우리가 만든 부모 오브젝트인 Spikes 오브젝트에 리지드바디 유무, 바디타입 등과 Spikes 오브젝트에 자식 오브젝트인 top, bottom에 리지드바디 유무, 바디타입 등에 따라서 오브젝트가 다양한 움직임을 보입니다. 여러분이 직접 넣어보고 어떤식으로 활요할지 확인해 보시는 것을 추천합니다.

저희는 Spikes 오브젝트와 top, bottom 오브젝트를 하나처럼 우직이게 하기 위해서 Spikes 오브젝트에만 리지드 바디를 추가했습니다.

다음에 포스팅할 기회가 생기면 더 자세하게 다뤄보겠습니다.




## 이벤트 함수의 실행순서

대망의 C#스크립트를 보기 앞서서 먼저 설명 하겠습니다.
Unity 스크립트를 실행하면 사전에 지정한 순서대로 여러 개의 이벤트 함수가 실행됩니다. 자세하게 알고 싶으신 분은 밑은 버튼을 눌러주세요.

[이벤트함수의실행순서](https://docs.unity3d.com/kr/current/Manual/ExecutionOrder.html){: .btn .btn--info}

간단하게 설명하면 아래의 이미지처럼 스크립트의 수명 주기 동안 이벤트 함수의 순서를 지정하고 반복합니다. 

![scriptlifecycle](https://docs.unity3d.com/kr/current/uploads/Main/monobehaviour_flowchart.svg)

## C# 스크립트
드디어 대망의 스크립트입니다. 스크립트는 게임 오브젝트의 동작을 정의하는 컴포넌트입니다. 



![script01](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird03/script01.png?raw=true)
프로젝트창에서 Assets 를 선택 후 우클릭 > Create > C# script 를 통해 스크립트를 생성합니다. 이 때 이름을 바로 정해주면 파일이름과 클래스 이름이 같게 만들어져서 편합니다. **파일이름과 클래스 이름이 다를 경우 스크립트가 작동을 안합니다.** 저는 PlayerController로 만들었습니다.



![script02](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird03/script02.png?raw=true)

만들어진 스크립트를 더블 클릭 하면 위의 이미지와 같이 저희가 코딩할 때 자주보던 창을 확인할 수 있습니다.

보시면 public class PlayerController : MonoBehaviour 로 작성되어 있습니다. PlayerController는 MonoBehaviour를 상속받는 것을 의미합니다. MonoBehaviour 클래스를 통해서 정의된 유용한 함수들을 사용할 수 있습니다. 아래의 버튼은 MonoBehaviour도큐멘트 입니다. 들어가보셔서 함수들을 확인해 보시면 좋을거 같습니다.

[MonoBehaviour](https://docs.unity3d.com/kr/current/ScriptReference/MonoBehaviour.html){: .btn .btn--info}



```c#
public class PlayerController : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        Debug.Log("Start");
    }

    // Update is called once per frame
    void Update()
    {
        Debug.Log("Update");
    }
}

```

위와 같이 코딩해주시고, 저장 후 PlayerController 스크립트를 Player 오브젝트 인스펙터창에 드래그 앤 드랍 해줍니다. 그리고 게임을 실행시켜 보겠습니다.



![script03](https://github.com/DozeKR/DozeKR.github.io/blob/master/images/2023-02-15-unity_flappybird03/script03.png?raw=true)

콘솔창에서 Start 게임 시작 때 한 번 그리고 매 프레임마다 Update가 뜨는 것을 확인할 수 있습니다. 이렇게 C#스크립트는 이벤트의 실행 순서에 맞춰 반복하여 동작합니다.



# 정리
1. 프리팹(Prefab): 콜라이더는 충돌 영역을 감지하는 컴포넌트입니다.
2. (상속)부모-자식 관계: 리지드바디는 물리엔진을 사용할수 
3. C# 스크립트 이벤트의 실행 순서에 맞춰 반복하여 동작
