---
title: "[Study] StudyFork 6주 차 기록"
date: 2020-07-15T00:35:28+09:00
tags: ["Study", "Android", "Tips", "ViewModel", "LiveData"]
keywords: []
description: "ViewModel 은 rotate 시 destory 된 액티비티의 컨텍스트를 계속 가지고 있어서 컨텍스트를 사용할 시 액티비티 컨텍스트가 아닌 Application Context 를 사용 할 것
-   ViewModelStoreOwner : 내가 만든걸 저장시키고 가지고 옮"
draft: false
---

## ViewModel

[https://developer.android.com/topic/libraries/architecture/viewmodel?hl=en](https://developer.android.com/topic/libraries/architecture/viewmodel?hl=en)

-   ViewModel 은 rotate 시 destory 된 액티비티의 컨텍스트를 계속 가지고 있어서 컨텍스트를 사용할 시 액티비티 컨텍스트가 아닌 Application Context 를 사용 할 것
-   ViewModelStoreOwner : 내가 만든걸 저장시키고 가지고 옮
-   Map 으로 관리하여 Owner 에 따라 같은 Owner 를 넣을 경우 같은 viewModel 객체를 가질 수 있음. -> Observe 한 객체의 내용 바로반영 가능
-   Activity 와 Fragment 일 경우 Owner 를 각각 Activity , Fragment 로 주면 다른 ViewModel 객체를 가지게 됨

## LiveData

-   onPause onStop 시 데이터를 배출하지 않음
-   onStart , onResume 으로 돌아가면 배출 (active 한 상태에서만 데이터를 배출)
-   binding 된 viewmodel 에도 lifeCycleOwner 를 넣어주어야 함. (필수)
-   viewModel 내부에서 private val 은 MutableLiveData 를, public 은 LIveData 를 ( private val\_text, public text )
-   MediatorLiveData : addSource(text2) {"$text2 입니다.".}
-   Transformations.map(text2) {"$text2 입니다." }, text2.observeForever {text3.value = text2.value}

### LiveData 의 Rx

-   계속 돌아가는 (예 1초마다 숫자증가) LiveData 는 Activity 가 Destroy 되어도 살아있기 때문에 dispose 해주어야 한다.
-   CompositedDisposable 을 이용하여 Observe를 add 해주고 onCleared 에서 dispose() or clear() 를 해준다.
    -   disposite : 객체를 다시 쓸 수 없음
    -   clear : 객체를 다시 사용할 수 있음 (권장)

### Fragment life cycle

-   fragment life cycle 과 fragment 의 view 들의 cycle 이 다름
-   fragment 의 lifecyclerOwner 는 viewLifeCyclerOwner 를 사용

## TIP!

-   MvnRepository : maven 라이브러리의 버전들을 볼 수 있음

### 레이아웃

개발자 모드에서 레이아웃 점유 현황을 보이게 할 수 있음

### todo, fixme (Live Templates)

-   LIve Templates - AndroidComments - todo, fixme 의 아래에 Change 에서 Kotlin 추가해준다
-   Activity 를 입력하면 바로 만들어둔 형식이 나오게 하는 등 커스텀 가능 $todo$ 를 사용하면 바로 그 자리에 포인터깜빡임

### 파일탐색

alt+f1 => 파일탐색  
ctrl + e => 최근파일  
ctrl + alt + home => 자바만 됨. xml 에서 바로 activity 갈 수 있음. 반대도 가능  
shift + ctrl + alt + j => 단어 전체 변경 가능

---
<footnote>2019.12 ~ 2020.02 까지의 스터디 기록</footnote>