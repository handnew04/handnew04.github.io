---
title: "[Study] StudyFork 2주 차 기록"
date: 2020-07-15T00:29:39+09:00
tags: ["Study", "Android"]
keywords: []
description: "onClick set 은 create 에서 (viewHolder 에서)  
viewholder 내부에서 bind 시 데이터타입 받을 때 동작할 함수를 생성해서  
url 의 변경만 bind 에서  
인터페이스 방법은 '리스너 패턴'"
draft: false
---

**Recyclerview**  
onClick set 은 create 에서 (viewHolder 에서)  
viewholder 내부에서 bind 시 데이터타입 받을 때 동작할 함수를 생성해서  
url 의 변경만 bind 에서  
인터페이스 방법은 '리스너 패턴'

## 데이터 모델

m 데이터를 v view에 p(vm….) 어떻게 뿌릴 건가

### DataSource - Remote, Local

view - in, out 의 입력받고 보여주는 일을 하는데 Activity 에서 retrofit 을 쓰면서 커짐

ex)

```
class NaverRemoteDataSource { 
    val naverApiService
    fun queryMovie(query : String, 콜백받을 오브젝트??) {
    naverApi.searchMovie(query)) //retrofitService 의 return 값 Call<T>
            .enque(
            fun success(){}
            fun fail(){}
        )
    }
}
```

Call : retrofit Class  
Callback

#### Repository

-   data를 Remote 에서 가져올지 Local 에서 가져올지 결정
-   어떻게 저장하고 보여줄건지 결정
-   local 데이터를 먼저 뿌릴지 말지 결정, 업데이트가 필요시 remote 에 요청
-   Activity -> Repository -> Remote/Local DataSource
-   Remote Data -> local 저장 (Local DataSource 에 보냄, LocalDataSource 에서 저장처리)-> activity 보여줌

**data pakage ex**  
data.repository  
data.source.remote  
data.source.local

MovieRemoteDataResource  
MovieRemoteDataResourceImpl

**etc**  
kotlin high order fun  
tools -> kotlin -> byteCode -> Decompile 자바로 돌아가는 모습 확인 가능  
findViewbyId 대신 data Binding

---
<footnote>2019.12 ~ 2020.02 까지의 스터디 기록</footnote>