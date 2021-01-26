---
layout: post
comments: true
date: 2021-01-26 18:00:20
title: "유니티 레이케스트"
description: "RaycastHit2D"
subject: dev
categories: [ Unity ]
tags: [ unity, raycast, RaycastHit2D ]
---


`Raycast` 와 `Raycast2D` 의 다른점은 Z값을 사용하냐 사용하지 않느냐의 차이밖에 없다.

3차원 공간에서 어느 한 점(시작점)에서  Ray 를 정해진 방향으로 쏴 Ray 와 충돌 되는 객체를 구하는 방법이다.

![RaycastHit2D Physics2D.Raycast(Vector2 origin, Vector2 direction, float distance, int layerMask)](/images/dev/unity-raycasting.jpg "RaycastHit2D Physics2D.Raycast(Vector2 origin, Vector2 direction, float distance, int layerMask)")

<br>

### 탑다운 2D 레이케이스트 예제

```c#
Vector3 dirVec;
GameObject scanObject;


void Update(){
    // Direction
    if(vDown && v == 1){
        dirVec = Vector3.up;
    }else if(vDown && v == -1){
        dirVec = Vector3.down;
    }else if(hDown && h == 1){
        dirVec = Vector3.right;
    }else if(hDown && h == -1){
        dirVec = Vector3.left;
    }
    
    // Raycast
    Debug.DrawRay(rigid.position, dirVec * 0.7f, new Color(0,1,0));
    RaycastHit2D rayHit = Physics2D.Raycast(rigid.position, dirVec, 0.7f, LayerMask.GetMask("Object"));

    // Scan Object
    if(Input.GetButtonDown("Jump") && scanObject != null){
        Debug.Log("this is : " + scanObject.name);
    }
}
```




