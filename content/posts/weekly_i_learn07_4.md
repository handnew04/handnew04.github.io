---
title: "[WIL] 7월 4주차"
date: 2019-08-13T22:10:43+09:00
tags: ["WIL","SQL","safe update mode", "Swagger","static","비트","비트연산","codeStyle","LocalBroadcastManager"]
keywords: []
description: 'Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column.  To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.'
draft: false
---
## SQL safe update mode error
- Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column.  To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.
- 하나의 레코드만을 update, delete 하도록 설정 된 모드인데 다수의 레코드를 수정하려 할때 에러 발생. 
- 일시적 safe 모드 해제 : set sql_sate_updates=0;
- 영구적 해제는 워크벤치의 file - preference에서 safe mode 를 해제하면 된다.
- 쿼리문 실행시 조건으로 프라이머리키의 true 조건을 추가 해주면 간단히 해결 (ex where %%%  and  primarykey > 0)


## Swagger
- http://localhost/swagger-ui.html
- login 및 api 요청시 돌아오는 json 확인 가능


## static method 안에서 전역 변수, 메소드 사용하기 

- static 메소드 사용시 (ex Handler) 액티비티나 프래그먼트를 파라미터로 받음
- (mFragment.get()).변수 또는 mActivity.get().메소드 등으로 사용 가능


## 비트와 비트연산
- [비트와 비트연산 참고](https://duvallee.blog.me/221438708741)


## CodeStyle Android
- [코드스타일 참고](https://github.com/ribot/android-guidelines/blob/master/project_and_code_guidelines.md)


## LocalBroadcastManager
- 일반 브로드캐스트를 말할 때의 브로드캐스트는 보통 글로벌 브로드 캐스트로 방송이 안드로이드 내에 등록된 모든 리시버에게 전달 된다. (프로세스 경계x)
- 로컬 브로드캐스트의 경우 현재 프로세스 안에서만 유효한 브로드캐스트로 앱의 정보를 밖으로 유출하지 않는다. 
- 아래와 같이 등록하여 사용, 브로드캐스트리시버와 같이 sendBroadcast(intent); 로 전달 가능 
```
LocalBroadcastManager.getInstance(context).registerReceiver(Receiver,intentFilter); 
```
