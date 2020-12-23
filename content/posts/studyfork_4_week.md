---
title: "[Study] StudyFork 4주 차 기록"
date: 2020-07-15T00:30:10+09:00
tags: ["Study", "Android", "DataBinding"]
keywords: ["two way binding 객체와 view 서로 주고 받은 바인딩 @={} : two way  @{} : one way 로 구분 예를 들어 EditText 의 내용을 객체로 바로 보내서 바로 TextView 로 보여줄 수 있음  set 은 int 로 get은 string 의 경우에도 사용"]
description: "객체와 view 서로 주고 받은 바인딩 @={} : two way  @{} : one way 로 구분 예를 들어 EditText 의 내용을 객체로 바로 보내서 바로 TextView 로 보여줄 수 있음  set 은 int 로 get은 string 의 경우에도 사용"
draft: false
---

**[https://developer.android.com/topic/libraries/data-binding/generated-binding](https://developer.android.com/topic/libraries/data-binding/generated-binding)  [https://developer.android.com/topic/libraries/data-binding/expressions](https://developer.android.com/topic/libraries/data-binding/expressions)**

## two way binding

객체와 view 서로 주고 받은 바인딩 @={} : two way  @{} : one way 로 구분 예를 들어 EditText 의 내용을 객체로 바로 보내서 바로 TextView 로 보여줄 수 있음  set 은 int 로 get은 string 의 경우에도 사용

## BR

R 처럼 Binding Resource 인것.. xml 의 data 에 선언하면 BR에 등록 되는데  BR.name 으로 사용 가능  아래의 두 코드가 같은 의미

1.  binding.name = ""
    
2.  binding.setVariable(BR.name, "")

---
<footnote>2019.12 ~ 2020.02 까지의 스터디 기록</footnote>