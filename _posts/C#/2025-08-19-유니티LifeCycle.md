---
title: "유니티 생명주기 함수"
excerpt: "이벤트 함수의 실행 순서(Life Cycle)"

categories:
  - Unity

permalink: /Unity/lifecycle/

toc: true
toc_sticky: true

date: 2025-07-19
last_modified_at: 2025-08-19
---

## 유니티 생명주기 함수란?

**유니티 엔진에서 스크립트의 객체가 생성되고 활성화, 업데이트, 비활성화, 파괴되는 과정에서 자동으로 호출되는 함수**를 뜻한다.\
대표적인 생명주기 함수로는 Awake, OnEnable, Start, Update, FixedUpdate, LateUpdate, OnDisable, OnDestroy 등이 있다.

### 주요 생명주기 함수

> Awake
>> 스크립트 인스턴스 로드 직후 호출되는 함수. 오브젝트가 비활성이어도 호출되며, 오브젝트 초기화에 사용.

> OnEnable
>> 오브젝트가 활성화될 때마다 호출되는 함수.

> Start
>> 오브젝트가 활성화된 후 첫 번째 프레임 이전에 호출되는 함수.

> Update
>> 매 프레임 호출되는 함수. tick()과 동일.

> LateUpdate
>> 같은 프레임의 모든 Update 이후 호출되는 함수. 카메라 추적, 본 보정, 후처리 등에 사용.

> FixedUpdate
>> 고정 간격 틱마다 호출되는 함수. 물리 연산에 사용됨.

> OnApplicationQuit
>> 에디터에서 사용자가 플레이 모드를 중지할 때 또는 애플리케이션 종료 전 모든 게임 오브젝트에서 호출되는 함수. 

> OnDisable
>> 오브젝트가 비활성화될 때마다 호출되는 함수.

> OnDestroy
>> 오브젝트 파괴 또는 씬 언로드 직전 호출되는 함수.

> OnCollisionEnter/Stay/Exit
>> 비트리거 충돌체 접촉 시작/유지/종료 시 틱에 맞춰 호출되는 함수.

> OnTriggerEnter/Stay/Exit
>> 트리거 충돌체 접촉 시작/유지/종료 시 호출되는 함수.

<br>

## 생명주기 함수 호출 순서

![lifecycle](https://github.com/user-attachments/assets/f1ef984d-5de8-4d9b-9c55-a14238bc98fb)

[이벤트 함수의 실행 순서](https://docs.unity3d.com/kr/2019.4/Manual/ExecutionOrder.html)

기본적인 호출 순서는 위 이미지를 따른다.\
주요 함수들만 추려보자면 **Awake -> OnEnable -> Start -> FixedUpdate -> OnTriggerXXX
-> OnCollisionXXX -> Update -> LateUpdate -> OnApplicationQuit -> OnDisable -> OnDestroy**라고 볼 수 있다.

다만, FixedUpdate는 프레임과 독립적으로 물리 틱마다 끼어들며, 기본값은 0.02초이다.\
프레임이 느려지면 한 프레임 안에서 여러 번 호출되고, 프레임이 빨라지면 해당 프레임에선 호출되지 않을 수도 있다.
