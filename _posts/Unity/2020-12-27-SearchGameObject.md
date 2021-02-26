---
layout: post
comments: true
date: 2020-12-27 18:00:20
title: "특정 GameObject 찾는방법"
description: "How to Search GameObject"
subject: unity
categories: [ Unity ]
tags: [ unity, GameObject, search ]
---

## 특정 GameObject를 스크립트에서 반환 받기

조건
- 찾고자 하는 오브젝트는 개체화가 되어 있어야 함 (Hierarchy View에 표시되어 있는가).
- 찾고자 하는 오브젝트는 활성화(Activy)가 되어 있어야 함 (오브젝트의 Inspector View의 이름 옆 체크박스가 체크되어 있는가).

~~~cs
// Object의 이름으로 대상을 찾음, 이름이 같을 경우 가장 처음 검색된 Object 반환
GameObject obj1 = GameObject.Find("Name"); 

// 태그로 대상을 찾음, 이름이 같을 경우 가장 처음 검색된 Object 반환
GameObject obj2 = GameObject.FindWithTag("Tag"); 

// 같은 태그를 가진 Object들을 GameObject[] 형태로 반환
GameObject obj3 = GameObject.FindObjectsWithTag("Tag"); 
~~~

## 자식 오브젝트를 찾는 경우

조건
- 부모 오브젝트는 활성화가 되어 있어야 함.
- 자식 오브젝트는 비활성화 되어 있어도 무관.
  
~~~csharp
// Object의 이름을 찾음. 가장 처음에 나오는 Object를 반환.
GameObject obj1 = transform.Find("Name").gameObject;

// 자식을 번호로 찾음. 0번째가 첫 번째 자식 
GameObject obj2 = transform.GetChild(0).gameObject; 
~~~
Transform으로 찾는 경우, 반환 형이 Transform이므로 게임오브젝트를 참조하는 경우 Transform.gameobject​로 참조가 가능하다.


## 실사용 차이

- 성능적 측면에서 오브젝트를 찾는 함수는 Update()와 같이 프레임마다 호출하는 것은 좋지 않다.
- Tag를 사용하는 편이 속도가 더 빠르기 때문에 쓸 수 있는 상황에서는 GameObject.FindWithTag를 쓰는 편이 좋다.
(플레이어, 적 플레이어, 바닥, 벽 등을 찾을 때)
- 자주 활성, 비활성을 작업 해주는 오브젝트는 활성화된 부모 오브젝트를 두어 계속 접근할 수 있게끔 해줘야 한다.
(이 때 Transform.Find를 사용 한다.)

## 메서드

### GameObject 클래스 메서드

함수

`Find` : 오브젝트 이름으로 검색하여 가장 처음에 나오는 오브젝트를 GameObject로 반환한다.

`FindWIthTag` : 태그 이름으로 검색해서 나타난 오브젝트 여러개를 GameObject 배열로 반환한다.

`FindGameObjectsWithTag` : 태그 이름으로 검색해서 나타난 오브젝트 여러개를 GameObject 배열로 반환한다.

`FindObjectOfType` : 오브젝트형(혹은 컴포넌트의 형)으로 검색해서 가장 처음 나타난 오브젝트를 GameObject로 반환한다. (유효한 오브젝트만)

`FindObjectsOfType` : 오브젝트형(혹은 컴포넌트의 형)으로 검색해서 가장 처음 나타난 오브젝트 여러개를 GameObject 배열로 반환한다. (유효한 오브젝트만)

### Transform 클래스 메서드

함수

`Find` : Object의 이름으로 자식 오브젝트를 검색해, 가장 처음에 나타난 자식 오브젝트를 반환한다.

`GetComponentInChildren` : 컴포넌트 형으로 자식 오브젝트를 검색해서 처음 나타난 자식 오브젝트를 반환한다.

`GetComponentsInChildren` : 컴포넌트 형으로 자식 오브젝트를 검색해서 나타난 자식 오브젝트들의 배열을 반환한다.

`GetComponentInParent` : 컴포넌트 형으로 부모 오브젝트를 검색해, 가장 처음에 나타난 부모 오브젝으를 반환한다.

`GetComponentsInParent` : 컴포넌트 형으로 부모오브젝트를 검색해서 나타난 부모 오브젝트들의 배열을 반환한다.

`FindObjectOfType` : 오브젝트형(혹은 컴포넌트의 형)으로 검색해서 가장 처음 나타난 오브젝트를 반환한다. (유효한 오브젝트만)

`Transform.FindObjectsOfType` : 오브젝트형(혹은 컴포넌트의 형)으로 검색해서 나타난 여러개의 Object들을 배열의 형태로 반환한다. (유효한 오브젝트만)

---

참고 문헌 및 자료

https://cru6548.tistory.com/5

https://tenlie10.tistory.com/90

https://novemberfirst.tistory.com/4

https://docs.unity3d.com/ScriptReference/GameObject.Find.html

https://docs.unity3d.com/ScriptReference/GameObject.FindWithTag.html

https://m.blog.naver.com/os2dr/221556006710