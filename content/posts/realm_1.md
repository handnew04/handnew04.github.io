---
title: "[Realm] Realm 사용기"
date: 2019-12-23T23:01:36+09:00
tags: ["Android", "Realm"]
keywords: []
description: "기존의 SharedPreference + SQLite 로 이루어진 로컬db를 Realm 으로 교체하기 위함"
draft: false
---
-   기존의 SharedPreference + SQLite 로 이루어진 로컬db를 Realm 으로 교체하기 위함

### 특징

-   Realm 의 테이블은 java 에서 사용하는 클래스파일로 대체 된다.
    
    ```
    public class Sample extends RealmObject {
     private String vehicleId;
     private int vehicleName;
    }
    ```
    
-   클래스 내부에 필요한 컬럼을 넣을 수 있고 getter & setter 로 일반 클래스처럼(setter 는 트랜잭션 내에서만 가능) 사용할 수 있다.
    

### 사용하기

1.  [공식문서](https://realm.io/kr/docs/java/latest/#getting-started)
    
2.  컬럼마다 업데이트를 하던 기존 데이터베이스와 달리 지정한 PrimaryKey를 비교하여 존재하지 않으면 쓰기를, 존재하면 오브젝트 자체를 업데이트 할 수 있다.  
    realm.copyToRealmOrUpdate(RealmObject);
    
3.  RealmObject -> JSONObject 로 바꾸러면 Gson 등을 이용해야 하는데, 데이터베이스에서 불러온 객체의 경우 바로 gson 을 사용할 수가 없다. 이는 realm 의 무복제 메커니즘 때문인데, 실제 사용전에는 Java Heap 으로 복사되지 않는다. 그래서 실제 데이터를 사용해야할 때, 아래와 같이 복사하여 사용한다.
    
    ```
    RealmObjectSample sample = realm.where(RealmObjectSample.class).findFirst();
    sample = realm.copyFromRealm(sample);
    ```
    
4.  한 A(RealmObject 클래스) 안에 다른 B(RealmObject 객체)가 들어있다면 A를 realm 에 저장할 시 A객체 안의 B가 null 이 아니라면 B를 직접 B클래스에 인설트 하지 않아도, B 클래스 테이블 안에 B가 자동으로 저장된다.