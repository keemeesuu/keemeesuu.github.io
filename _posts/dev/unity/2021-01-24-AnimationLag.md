---
layout: post
comments: true
date: 2021-01-23 18:00:20
title: "애니메이션 동작이 안될때"
description: "2D Sprite Atlas"
subject: dev
categories: [ Unity ]
tags: [ unity, awake, start, update, lateupdate ]
---


에니메이션 `Stat`(스테이트)에 들어오긴 했는데 애니메이션 재생이 안될때가 있다.(1% 정도 파란 프로그래스바 보임)

키를 꾹 누르고 있으면 값을 공급을 하는데 시작만 하고 재생을 못하는데 이럴때 해결하려면 `Transition`을 딱 한번만 줘야함.

Transition(State간의 화살표)을 연속적으로 태우면 애니메이션이 작동되지 않음


```c#

    // Move Value
    h = Input.GetAxisRaw("Horizontal");
    
    // Check Button Horizontal
    bool h = Input.GetButtonDown("Horizontal");

    // Animation
    anime.SetBook("isChnage", true);
    anime.SetFloat("hAxisRaw", h)

```

