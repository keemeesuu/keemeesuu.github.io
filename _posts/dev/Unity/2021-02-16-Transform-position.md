---
layout: post
comments: true
date: 2021-02-16 21:00:20
title: "transform.position, transform.translate"
# description: "Unity API"
subject: dev
categories: [ Unity ]
tags: [ unity, transform, position ]
---

# 1.transform

`transform`은 게임 오브젝트의 위치, 회전 그리고 스케일(Scale)을 나타낸다.

유니티에서 모든 오브젝트는 `trnsform`을 가지고 있다.

`transform`의 상태 값을 변경하여, 오브젝트의 이동, 회정 등을 하게 된다.

오브젝트를 이동하는 것은 이 `transform`의 위치를 변경해 주므로서 이뤄진다.

<br>

## 1.1 position 과 Translate()의 차이

`transform.position` : 월드 좌표값이며, 월드 좌표를 기준으로 오브젝트를 이동시킨다

`transform.Translate` : 로컬 좌표값으로, 오브젝트를 기준으로 물체를 이동시킨다.


이는 다시 말해, `position`은 이동 대상이 되는 물체의 회전값에 영향을 받지않고 이동하며,

`translate`은 물체의 회전값에 영향을 받아 이동한다는 것이다. 

<br>

## 1.2 transform.position

`position`을 이용해 물체의 이동을 구현한다.

`Update()`가 발생할때마다, x축으로 10만큼 이동한다.


```c#
void Update(){
    // 로컬 좌표 이동
    transform.position = transform.position + new Vector3(10, 0, 0);

    // 월드 좌표 이동
    transform.position = new Vector3(10, 0, 0);
}
```

## 1.3 transform.Translate()

오브젝트의 transform의 Translate() 함수를 이용하여 이동을 구현한다.

Translate()를 이용해 x좌표의 10만큼 물체를 이동시킨다.

Translate()의 두번째 인자 값으로 물체의 로컬좌표 이동을 월드좌표로 이동하도록 구현한다.

public void Translate(Vector3 translation, Space relativeTo = Space.Self);


```c#
void Update(){
    // 로컬 좌표 이동
    transform.translate(new Vector3(10, 0, 0));

    // 월드 좌표 이동
    transform.translate(new Vector3(10, 0, 0), space.World);
}
```



## 1.4 절대적 이동

글로벌 좌표에서 현재 position을 x=0, y=10, z=0 만큼 이동시킨다.

```c#
transform.position = new Vector3(0, 10, 0);
```

<br>

## 1.5 상대적 이동

부모 position의 상대적인 위치로, 부모에서 부터 x=0, y=10, z=0 만큼 이동시킨다.

부모 position 값이 (0, 10, 0) 이면 자식 position값이 (0, 5, 0) 이라면,

자식 오브젝트의 월드 스페이스 좌표는 (0, 15, 0)이 된다.

```c#
transform.position = new Vector3(0, 10, 0);
```

<br>
<br>
<br>
<br>


[참고문헌](https://notyu.tistory.com/23){:target="_blank"}

[공식 레퍼런스](https://docs.unity3d.com/ScriptReference/Transform-position.html){:target="_blank"}

[Transform.Translate - 공식 레퍼런스](https://docs.unity3d.com/kr/530/ScriptReference/Transform.Translate.html){:target="_blank"}