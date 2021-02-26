---
layout: post
comments: true
date: 2020-12-24 18:00:20
title: "Awake, Start 차이점"
description: "Awake / start"
subject: unity
categories: [ Unity ]
tags: [ unity, awake, start ]
---

# Awake,Start

유니티에서 지정한 함수로서 초기화시 사용되는 함수들이다. 단 한번만 호출된다.

`Awake`
인스펙터창에서 스크립트요소를 비활성화 해도 실행된다. 스크립트와 초기화 사이의 모든 레퍼런스 설정에 이용

`Start`
Awake다음으로 첫 업데이트 직전에 호출되지만 스크립트 요소가 활성화 상태여야 합니다.

예))

Awake: 적들에게 총의 총알을 초기화한다.(Set)

Start:적들에게 총을 쏳을 능력을 부여할때
