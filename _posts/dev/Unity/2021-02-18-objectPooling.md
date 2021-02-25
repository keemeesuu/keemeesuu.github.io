---
layout: post
comments: true
date: 2021-02-18 21:00:20
title: "오브젝트풀링(objectPooling) 사용예제"
# description: "Unity API"
subject: unity
categories: [ Unity ]
tags: [ unity, objectPooling, position ]
---

프리팹을 사용해서 `Instantiate`, `Destory` 을 할 경우 메모리를 계속 차지하면서 `Destory`을 해도 쓰레기 메모리를 남기게 된다.

즉, 생성과 삭제를 하면서 조각난 메모리가 쌓인다. 그렇게 쌓이고 쌓이다 보면 유니티엔진내의 기술인 가비지컬렉트(GC:쌓인 조각남 메모리를 비우는 기술)가 실행되면 게임자체내에서 살짝 렉처럼 끊기게 된다.

그걸 방지하기 위해 `objectPooling`(오브젝트 풀링)을 만들어야 한다.

`objectPooling` : 미리 생성해둔 풀에서 활성화/비활성화로 사용

`objectPooling` 으로 첫 로딩시간이 생기지만 중간에 끊기는 일을 방지한다.

첫 로딩 시간 = 장면 배치 + 오브젝트 풀 생성


### 사용예제

다양한 오브젝트풀링 기법이 있지만 간단한 예

```c#

public class ObjectManager : MonoBehaviour
{
    // 프리펩 변수 선언
    public GameObject enemyPrefab;
    public GameObject itemPrefab;
    public GameObject bulletPlayerPrefab;

    // 프리펩을 생성하여 저장할 배열 변수 생성
    GameObject[] enemy;
    GameObject[] item;
    GameObject[] bulletPlayer;

    // 오브젝트 풀을 배열에 담아 처리하기위한 변수
    GameObject[] targetPool;

    // 초기화 작업을 위한 함수
    void Awake(){
        /*
        * 초기화 작업
        * 한번에 등장할 개수를 고려햐여 배열 길이를 할당해준다
        * 첫 로딩 시간 = 장면배치 + 오브젝트 풀 생성
        */
        enemy = new GameObject[10];
        item = new GameObject[10];
        bulletPlayer = new GameObject[10];

        Generate();
    }

    
    // 오브젝트 생성을 위한 함수
    void Generate()(){
        // 생성(Instantiate)후 오브젝트를 비활성화 시켜준다

        // #1.Enemy
        for(int i=0; i<enemy; i++){
            enemy[i] = Instantiate(enemy);
            enemy[i] = setActive(false);
        }
        // #2.Item
        for(int i=0; i<item; i++){
            item[i] = Instantiate(item);
            item[i] = setActive(false);
        }
        // #3.Bullet
        for(int i=0; i<bulletPlayer; i++){
            bulletPlayer[i] = Instantiate(bulletPlayer);
            bulletPlayer[i] = setActive(false);
        }
    }

    // 외부(다른 스크립트)에서 오브젝트 풀에 접근할 수 있는 함수 생성
    public GameObject MakeObj(string type){

        switch(type){
            case "Enemy":
                targetPool = enemy;
                break;
            case "item":
                targetPool = item;
                break;
            case "BulletPlayer":
                targetPool = bulletPlayer;
                break;
        }

        // 비활성화 오브젝트를 활성화 시켜준 후 반환시킨다.
        for(int i=0; i < targetPool; i++){
            if(!targetPool.activeSelf){
                targetPool[i].SetActive(true);
                return targetPool[i];
            }
        }

        return null;
    }


    // 해당 오브젝트들을 전부 가져오는 함수
    // Tag로 가져올경우 부하가 올 수 있음으로 이렇게 사용한다.
    public GameObject[] GetPool(string type){

        switch(type){
            case "Enemy":
                targetPool = enemy;
                break;
            case "Item":
                targetPool = item;
                break;
            case "BulletPlayer":
                targetPool = bulletPlayer;
                break;
        }

        return targetPool;
    }

}
```