---
title: "[WIL] 7월 1주차"
date: 2019-07-22T22:38:06+09:00
tags: ["WIL","weakReference","AdvertisingIdClient"]
keywords: [""]
description: "핸들러를 이너 클래스로 사용 시 메모리 누수* 발생 가능. 그 상황을 방지 하는 역할 - 기존 핸들러 클래스를 static 클래스로 사용 - 핸들러 내부에서 해당 액티비티 타입의 WeakReference 변수를 생성하여 사용"
draft: false
---

## WeakReference

- 핸들러를 이너 클래스로 사용 시 메모리 누수* 발생 가능. 그 상황을 방지 하는 역할

- 기존 핸들러 클래스를 static 클래스로 사용

- 핸들러 내부에서 해당 액티비티 타입의 WeakReference 변수를 생성하여 사용

```java
   Private final WeakReference<StartActivity> mActivity;
```

- 메모리 누수

  - AsyncTask 가 제 할일을 마친 후, 사용하던 메모리를 다시 main 에게 돌려 주어야 하는데, 그러지 않는 경우  

## AdvertisingIdClient

class

- 구글의 플레이 서비스를 사용하는 디바이스의 ad ID를 얻을 수 있음
- 유저 식별용으로 적합
