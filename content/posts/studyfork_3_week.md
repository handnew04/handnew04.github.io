---
title: "[Study] StudyFork 3주 차 기록"
date: 2020-07-15T00:29:58+09:00
tags: ["Study", "Android", "MVP"]
keywords: ["MVP"]
description: "view 는 항상 in/out 만 할 것
-   in/out 외 다른 작업들은 모두 presenter 가 처리
-   presenter 가 M(model) 과 작업"
draft: false
---

## MVP

-   view 는 항상 in/out 만 할 것
-   in/out 외 다른 작업들은 모두 presenter 가 처리
-   presenter 가 M(model) 과 작업
-   view에는 각각의 함수만 존재 (성공, 아이디없음, 등)
-   presenter 에서 분기를 가지고 해당 분기에 대한 view 함수만 호출 (view 에는 분기가 없음)
    -   presenter 에서 성공시 -> view 의 성공함수 호출
    -   presenter 에서 아이디 없음 -> view의 아이디없음 함수 호출
-   view 와 presenter 가 서로를 알고 있음 (1:1 대응, 액티비티/프래그먼트 하나당 presenter 하나 생성)
    -   추가 :: presenter 가 생성자의 인자값으로 view를 가지고, view에서 presenter 객체를 생성하면서 view.this 를 전달하게 됨
-   presenter 에서 repository 를 호출하는데 이 때 repository 는 싱글톤의 형태가 좋음
    -   repository가 인스턴스마다 다른 역할을 하는 것이 아니기 때문에 싱글톤이 좋음
-   Contract (interface) 가 view와 presenter 사이의 소통 담당
-   Contract 내부에 viw 와 presenter interface 를 가짐
-   presenter 에선 Contract.View 객체를 가지고 있음 (Contract.View의 함수에만 접근가능하게 함)

---
<footnote>2019.12 ~ 2020.02 까지의 스터디 기록</footnote>