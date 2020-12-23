---
title: "[Study] StudyFork 7주 차 기록"
date: 2020-07-15T00:35:40+09:00
tags: ["Study", "Android"]
keywords: []
description: " Dependency Injection
-   의존을 밖에서 주입해주자.
-   [DI PPT 참고](https://jakewharton.com/dependency-injection-with-dagger)
-   벤다이어그램 연관 관계 참고 (외부에서 변수를 넣는지 내부 생성자에서 인스턴스화 하는지 등, 내부 생성시 객체 고정으로 변경 불가) -> DI 는 집약관계를 이용  "
draft: false
---

## DI

-   Dependency Injection
-   의존을 밖에서 주입해주자.
-   [DI PPT 참고](https://jakewharton.com/dependency-injection-with-dagger)
-   벤다이어그램 연관 관계 참고 (외부에서 변수를 넣는지 내부 생성자에서 인스턴스화 하는지 등, 내부 생성시 객체 고정으로 변경 불가) -> DI 는 집약관계를 이용  
    
-   @provides : 객체를 제공
-   @Module : 객체가 모여있는 곳
-   @Inject : 주입하겠다.

Dagger : 컴파일시 Providing Dependencies (관계 그래프)확인  
Koin : 런타임시 - 확인 (에러 날 가능성 있음)

## Koin Reference

[https://start.insert-koin.io/#/quickstart/kotlin](https://start.insert-koin.io/#/quickstart/kotlin)

### pakage  
di pakage

-   LocalModule
-   RemoteModule
-   ViewmodelModule

### viewModel Fragment

```
val viewmodel : by viewModel<MainViewModel>() {
get()으로 가져올 수 없는 변수에 대해 
val hashId = arguments?.getString(HASH) : error()
parametersOf(hashId)
}
viewModel의 생성자에 hashId 를 받아줌 
viwModel {MainVeiwModel(()-> {hashId, get(), get()})}
```

## Etc

[issue](https://github.com/StudyFork/GoogryAndroidArchitectureStudy/pull/462)

'단순 이벤트를 던지기 위한 용도라면 Unit으로 type 을 변경해주세요' 의 의미  
isEmptyKeyword 같은 변수는 단순히 keyword의 length 가 0 일 때 이벤트를 발생시키는 용도라  
false, true 의 구분이 필요없음으로 MutableLiveData() 으로 주면 된다.

-   Unit 을 들어가서 보면 String 으로 이루어져 있다.

---
_2019.12 ~ 2020.02 까지의 스터디 기록_