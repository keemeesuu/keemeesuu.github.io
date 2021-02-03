---
layout: post
comments: true
date: 2021-02-03 15:00:20
title: "모바일 이동버튼 구현 - 이벤트 트리거(Event Trigger)"
# description: "Unity API"
subject: dev
categories: [ Unity ]
tags: [ unity, EventTrigger, event, trigger, charging ]
---

# 이벤트 트리거(Event Trigger)

### Pointer Down (BaseEventData)

UI에서 버튼을 게속 누르는 경우에 사용된다.

`Button` -> Inspector -> `Add Component` -> Event Trigger


<br>

한번 클릭할거 같으면

`Button` -> Inspector -> `On Click()` 에다가 `Add` 하면된다.

`On Click()` : ButtonDown + ButtonUp 한 세트




[공식 레퍼런스](https://docs.unity3d.com/ScriptReference/GameObject-activeSelf.html){:target="_blank"}