---
layout: post
comments: true
date: 2021-01-23 18:00:20
title: "스프라이트 아틀라스"
description: "2D Sprite Atlas"
subject: dev
categories: [ Unity ]
tags: [ unity, awake, start, update, lateupdate ]
---

개별적인 텍스처에 대해 리소스를 많이 소비하는 드로우콜이 발생하게 되는데 이것은 성능저하의 원인이 됩니다.

스프라이트 아틀라스(Sprite Atlas)는 여러 개의 텍스처를 단일 텍스처로 결합하는 에셋 입니다. 여러개의 드로우콜을 발행하는 대신 이러한 단일 텍스처를 호출함으로써 하나의 드로우콜을 발행할 수 있습니다.

## 아틀라스 자르기

1. `Sprite Mode` : Multiple
2. `Pixel Per Unit` : 한 칸에 들어갈 픽셀 갯수를 정해준다.
3. `Filter Mode` : `Point`는 픽셀 그래도 선명하게 처리해준다 이걸 선택하지 않으면 자동필터링 때문에 이미지가 흐리게 된다. 
4. `Aplly` 버튼 클릭
5. `Sprite Editer` 버튼 클릭 (스프라이트 정보를 편집할 수 있는 창)
6. `Slice` 버튼 클릭
7. `Grid By Cell Size` 클릭후 픽셀 사이즈와 패딩으로 여백간격을 조정하여 이미지를 잘라줌 잘 안보일 경우 `Apply` 오른쪽 버튼 클릭




참고자료

[2D 아틀라스와 애니메이션 - 골드메탈](https://youtu.be/IkvYstCzcoc){:target="_blank"}
