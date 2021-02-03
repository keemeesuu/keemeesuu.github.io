---
layout: post
comments: true
date: 2021-02-03 15:00:20
title: "PC, 모바일 이동버튼 구현 - 이벤트 트리거(Event Trigger)"
# description: "Unity API"
subject: dev
categories: [ Unity ]
tags: [ unity, EventTrigger, event, trigger, charging ]
---

# 이벤트 트리거(Event Trigger)

### Pointer Down (BaseEventData)

UI에서 버튼을 게속 누르는 경우에 사용된다.

`Button` -> Inspector -> `Add Component` -> Event Trigger


```c#
float h, v;
bool hDown, vDown, hUp, vUp;

// Mobile Key Var
int up_Value, down_Value, left_Value, right_Value;
bool up_Down, down_Down, left_Down, right_Down;
bool up_Up, down_Up, left_Up, right_Up;


void Update()
{
    // Move Value(PC+Mobile)
    h = Input.GetAxisRaw("Horizontal") + right_Value + left_Value; // 더하는 이유는 움직임 상쇄 때문에(동시에 누르면 1 -1 = 0)
    v = Input.GetAxisRaw("Vertical") + up_Value + down_Value;

    // Check Button Down & Up(PC+Mobile)
    hDown = Input.GetButtonDown("Horizontal") || right_Down || left_Down;
    vDown = Input.GetButtonDown("Vertical") || up_Down || down_Down;
    hUp = Input.GetButtonUp("Horizontal") || right_Up || left_Up;
    vUp = Input.GetButtonUp("Vertical") || up_Up || down_Up;

    // Check Horizontal Move
    if(hDown || vUp){
        // Debug.Log("가로 이어서 이동");
        isHorizonMove = true;
    }else if(vDown || hUp){
        // Debug.Log("세로 이어서 이동");
        isHorizonMove = false;
    }else if(hUp || vUp){
        // 현재 AxisRaw 값에 따라 수평, 수직 판단하여 해결
        isHorizonMove = h != 0;
    }

    // Animation
    if(anime.GetFloat("hAxisRaw") != h){
        anime.SetBool("isChange", true);
        anime.SetFloat("hAxisRaw", h);
    }else if(anime.GetFloat("vAxisRaw") != v){
        anime.SetBool("isChange", true);
        anime.SetFloat("vAxisRaw", v);
    }else{
        anime.SetBool("isChange", false);
    }

    // Mobile Var Init - 초기화 작업
    up_Down = false;
    down_Down = false;
    left_Down = false;
    right_Down = false;
    up_Up = false;
    down_Up = false;
    left_Up = false;
    right_Up = false;
}
void FixedUpdate(){
    // Move
    Vector2 moveVec = isHorizonMove ? new Vector2(h, 0) : new Vector2(0, v);
    rigid.velocity = moveVec * speed;
}
```


<br>

한번 클릭할거 같으면

`Button` -> Inspector -> `On Click()` 에다가 `Add` 하면된다.

`On Click()` : ButtonDown + ButtonUp 한 세트




[공식 레퍼런스](https://docs.unity3d.com/ScriptReference/GameObject-activeSelf.html){:target="_blank"}