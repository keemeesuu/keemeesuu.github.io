---
layout: post
comments: true
date: 2020-12-28 18:00:20
title: "이벤트 함수의 실행 순서(Awake, Start, Update, LateUpdate)"
description: "Awake, Start, Update, LateUpdate"
subject: dev
categories: [ unity ]
tags: [ unity, awake, start, update, lateupdate ]
---

## 이벤트 함수의 실행 순서
유니티 스크립팅시, 미리 정의된 순서대로 실행되는 이벤트 함수가 있습니다.

## 첫번째 씬 로드
이 함수는 씬이 시작되면 호출이됩니다(씬의 각 오브젝트에 대해 한 번).

- `Awake` : 이 함수는 항상 Start 함수의 이전 및 프리팹의 인스턴스화 직후에 호출됩니다. (만약 게임 오브젝트가 시작할 때 무효인 경우, 활성화되거나 연결된 하나의 스크립트 함수가 호출될 때까지, Awake는 호출되지 않습니다.)
- `Start` : Awake 다음으로 첫 업데이트 직전에 호출되지만 스크립트 요소가 활성화 상태여야 함. 
- `OnEnable` : (오브젝트가 활성화된 경우에만 호출됩니다): 이 함수는 오브젝트를 활성화 한 직후에 호출됩니다. 이것은 MonoBehaviour 인스턴스가 생성될 때, 예를 들어 레벨 로드 또는 스크립트 컴포넌트에 연결된 게임 오브젝트가 인스턴스화 될 때 발생합니다.



## 업데이트 순서
게임 로직 인터랙션, 애니메이션, 카메라 위치 등을 추적하는 경우, 각종 이벤트를 사용할 수 있습니다. 일반적인 패턴은 Update() 함수 내에서 대부분의 작업을 수행하는 것입니다만, 다른 함수도 사용할 수 있습니다.

- `FixedUpdate` : FixedUpdate()는 Update()보다 자주 호출되는 경우가 많습니다. 프레임 속도가 낮은 경우에는 프레임마다 여러 번 호출 할 수 있지만, 프레임 속도가 높을 경우 프레임간에 호출 할 수 없습니다. FixedUpdate() 직후에 모든 물리적 특성 계산 및 업데이트가 발생합니다. FixedUpdate()에서 이동 계산을 적용 할 때 Time.deltaTime 값을 곱할 필요는 없습니다. 이것은 프레임 속도와는 독립적으로 FixedUpdate()가 신뢰할 수있는 타이머에서 호출되기 때문 입니다. (주로 물리작업을 입력합니다.)
- `Update` : Update는 프레임마다 한 번씩 호출됩니다. 이것은 프레임의 업데이트에 대한 주요 기능입니다. (주로 키입력을 받습니다.)
- `LateUpdate` : LateUpdate()는 Update() 후 프레임마다 한 번씩 호출됩니다. Update()에서 수행되는 계산이 완료되면 LateUpdate() 함수가 시작 합니다. LateUpdate()의 일반적인 사용은 다음의 3인칭 카메라입니다. Update()에서 캐릭터를 이동하고 회전시킬 경우 LateUpdate()에서 카메라의 이동과 회전 계산을 수행할 수 있습니다. 이렇게하면 캐릭터가 카메라가 그 위치를 추적하기 전에 완전히 이동합니다.


참고 문헌 및 디테일
https://docs.unity3d.com/kr/530/Manual/ExecutionOrder.html
