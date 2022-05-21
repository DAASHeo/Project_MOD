# 멋쟁이사자처럼 X 넥슨 MOD Suppoters Hackathon 2주차 TIL

이번 2주차에서는 기본적이고 많이 쓰이는 Component와 Component의 Property에 대해서 학습하였다. 

Component에 대해서 학습하면서 많이 제작해보면서 다양한 Component를 접해야 능숙하게 내가 원하는 기능을 구현할 수 있겠다는 생각을 하게되었다. 

그렇다면 2주차 TIL 스타트~!
## 3. 기본 컴포넌트의 이해


### TransformComponent

![](https://velog.velcdn.com/images/eheo/post/ed0f61f9-f394-4d2b-bb10-60916792a0ee/image.png)

  - 월드 상에서 Entity가 어디에 위치해있는지를 나타내는 컴포넌트
  - 필수적인 컴포넌트(특수한 경우에만 예외)
  - TransformComponent 구성
`Position` : Entity의 위치
`Scale` : Entity의 크기
`Zrotation` : Entity의 회전값
부모-자식의 트리 구조로 서로 다른 Entity와의 계층 구조를 형성하고 있기 때문에 부모의 Transform component가 자식에게 상대적인 좌표로 반영된다. (But, 부모는 자식의 특성을 따라가지 않는다)
`WorldPosition` : 월드에서의 절대적 좌표값 
`World Z Rotation` : 월드에서의 절대적 회전값




## 4. 지형과 레이어의 이해


### Tile 
![](https://velog.velcdn.com/images/eheo/post/0899af33-f228-4151-83cb-a813db207139/image.png)
- Tile 그릴 때 scene 상단의 tab의  box fill을 선택하고 Scene에 드래그하면 드래그 크기만큼 채워진 tile이 그려짐(마우스 우클릭으로 타일 드래그 시 삭제)

### TileMapComponent
![](https://velog.velcdn.com/images/eheo/post/e7ca13a5-f365-4ada-ae15-332b7e73d8b4/image.png)

- `Color` : 타일의 색상을 지정할 수 있는 property
- `FootholdDrag` : 타일맵 위에 있는 캐릭터의 마찰력 변화시킴(값이 클수록 빠르게 감속)
- `FootholdForce` : 타일맵 위에 있는 캐릭터에 가하는 힘(양수일 경우 오른쪽, 음수일 경우 왼쪽으로 힘을 받음)
- `FootholdWalk` : 타일맵 위에 있는 캐릭터의 속력 변화시킴(값이 클수록 빨라짐)
- `TileSetRUID` : 타일의 종류 선택할 수 있음

_✨ TMI :  Foothold와 관련된 property를 보고 인내의 숲이 생각났다...(넥슨의 진정한 갓게임) ✨_

### Foot Hold
- 움직임이 있는 Entity(몬스터, 캐릭터)가 밟을 수 있는 발판 정보
- File > Settings > 만들기 > 발판 정보를 설정하면 빨간색 선이 엔티티에 표시된다.<br><br>
![](https://velog.velcdn.com/images/eheo/post/74d11136-270c-4abe-bd1e-b68ac64db140/image.png)

![](https://velog.velcdn.com/images/eheo/post/552c7586-21bb-4cb5-9210-3e39a5d17a4d/image.png)

선을 조정하여 foot hold를 조정할 수 있다. <br>
![](https://velog.velcdn.com/images/eheo/post/698bfacb-6b60-4471-b9e1-9709c72f5a62/image.png)



## 5. 자주 사용하는 컴포넌트

Workspace > DefaultPlayer : 내 캐릭터 속성

### TweenComponent
: Entity에 운동성을 만들고, 세부 설정을 조정할 수 있다(설정된 출발지에서 목적지까지 이동)

1. TweenFloatingComponent : 원점을 기준으로 부유 운동
2. TweenCircularComponent : 원점을 중심으로 원운동
3. TweenLineComponent : 원점에서 목적지까지의 선형운동


### RigidbodyComponent
: 강체(형태가 변하지 않는 유체), 일반적인 고체의 물리적인 속성들을 컨트롤 하는 컴포넌트

- `Gravity` : 중력값. 공중에서 이동할 때에 지상으로 얼마나 빨리 떨어질 것인가와 연관이 있음(입력값이 높을수록 더욱 빠르게 떨어짐)

 **❗️Entity마다 가진 원점이 다르므로 중력을 줬을때 떨어지는 위치가 다름❗️**

- `IaBlockVerticalLine` : 기존 메이플 스토리 이동의 경우 세로 지형 타일이 연결된 것만 foothold로 인해 막히지만 이 property가 true일 경우 세로 지형이 무조건 Block이 된다. 벽 같은 지형을 무조건 통과할 수 없도록 할 때 사용된다.

- `IaBlockVerticalLine` : 기본 이동 규칙을 쿼터뷰 이동으로 변경(수평, 수직 이동 가능)

### MovementComponent
: 걷는 속도와 점프 높이를 수정할 수 있는 기능

- `InputSpeed` : 조작의 X축 힘(값이 증가할수록 이동 속도가 올라감)

- `JumpForce` : 조작의 Y축 힘(값이 증가할수록 더 높게 점프)

-> MovementComponent를 비활성화하면 state는 변하지만 이동은 안함(연출이 필요하거나 스킬에 따라서 일시적으로 비활성화할 수 있음)

### TriggerCompnent
: TriggerComponent를 가진 객체간의 충돌이 발생했을 때 이를 알려주는 컴포넌트


### PlayerComponent
: 캐릭터의 Hp나 PVPmode를 설정할 수 있음
- `MaxHp` : 최대 Hp

- `PVPmode` : true일 경우, 플레이어간 공격이 가능함
 

### PlayerControllerComponent
: 캐릭터의 이동 컨트롤을 부여할 수 있다.
- `AlwaysMovingState` : 이동 가능한 상태를 나타냄

- `FixedLoookAt` : 이동 시에 바라보는 방향을 한쪽으로 고정(0일 경우 양쪽을 바라볼 수 있고, 1일 경우에는 왼쪽만, -1일 경우 오른쪽만 바라볼 수 있음)
