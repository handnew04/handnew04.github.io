---
title: "[WIL] 7월 3주차"
date: 2019-07-22T23:06:14+09:00
tags: ["WIL","logCat","font","codeReview"]
keywords: []
description: '안드로이드 스튜디오의 Ffile - Setting-Editor-Color Scheme- Android Logcat 에서 톱니바퀴를 눌러 import 를 하거나 나의 색상을 export 하여 테마를 저장할 수 있다.'
draft: false
---

## Logcat 색상 설정
- 안드로이드 스튜디오의 Ffile - Setting-Editor-Color Scheme- Android Logcat 에서 톱니바퀴를 눌러 import 를 하거나 나의 색상을 export 하여 테마를 저장할 수 있다.



## 프로젝트 전체 폰트 적용 방법
- 앱에서 기본으로 사용할 폰트의 경우 전체 적용이 필요하다
- style.xml 에서 해당 앱의 베이스테마에 fontFamily 태그를 추가하여 사용할 폰트를 기입
- 다만 적용 되지 않는 다이얼로그 존재가 가능하며 그 부분에 대해선 해당 TextView 의 스타일이나 layout의 xml 파일에서 직접 추가 필요
- layout에서 theme 으로 수정한 앱테마를 받고있는지를 확인 -> 받는다면 적용됨



## review
1. for문 안에 for 문이 또 들어가는 등. 시간 복잡도가 n제곱으로 뛰는 작업은 찢어 놓는것이 좋다. -> 느려짐
2. 라이브러리 사용시 gradle 확인 할 것



## review
1. 다이얼로그 이너클래스를 따로 클래스파일로 뺄 것
2. 두군데 이상 사용하는 것 또는 같은 기능을 하는 변수들을 모아둔 클래스에 같이 static으로 정리할 것 
	- 구분 짓는 변수를 int 로 사용하는 것이 string 보다 좋음
	- 변수 명은 띄어쓰기 부분에 언더바를 사용 EDITNICKNAME  -> EDIT_NICKNAME
3. 공통적으로 사용하는 메서드는 하나의 클래스에 따로 빼는 것이 좋다.


