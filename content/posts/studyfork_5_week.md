---
title: "[Study] StudyFork 5주 차 기록"
date: 2020-07-15T00:35:18+09:00
tags: ["Study", "Android", "MVVM", "Observer"]
keywords: []
description: "pagination
endlessScrollListener  
쓰레쉬 홀더 ? 를 조정 -> 5 면 5개 남았을 때 재로딩"
draft: false
---

## pagination

endlessScrollListener  
쓰레쉬 홀더 ? 를 조정 -> 5 면 5개 남았을 때 재로딩

## 옵저버 패턴

-   유튜버 -> Youtube -> 구독자들
-   VM이 옵저버 객체에게 데이터를 바꿔서 넣어주면 옵저버 객체를 보고있던 V 들에게 바뀐 데이터를 알게 해줌
-   V가 옵저버 객체를 옵저빙 하고 있다.
-   One Way 일 경우 immutable , Two Way 일 경우 mmutable (밖에서 넣어야 하니까)

## Two way Binding 주의 사항

vm 에서 editText 로 알려줄때 old 와 new 가 다를 때만 알려주어야 함 (setText의 기존의 함수를 오버라이딩 할 때 기존의 setText 의 내용을 함께 사용 해야 한다.)

## MVVM

-   ViewModel 은 View 를 모른 상태로 구현 (MVP 의 V 와 P의 1:1 연결의 개선)
    -   그러나 복잡해질수록 결국 1:1 의 형태가 됨
-   Kotlin Delegates.observable
-   모든 데이터는 뷰모델이 주체 (뷰에서 가져오는 데이터들은 뷰모델이 갖고 있고 뷰모델의 데이터를 사용)
-   recyclerView.adapter 에 setItem 만들 때 adapter 를 BaseAdapter 를 만들어 상속 받아서  
    as BaseAdapter 하면 어댑터를 매번 새로 만들지 않아도 됨 !

    ---
<footnote>2019.12 ~ 2020.02 까지의 스터디 기록</footnote>