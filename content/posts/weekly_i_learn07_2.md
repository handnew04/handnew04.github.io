---
title: "[WIL] 7월 2주차"
date: 2019-07-22T23:01:20+09:00
tags: ["WIL","R","error","windowSoftInputMode","해상도","keyDown","lifeCycle"]
keywords: []
description: file 의 Invalidate Caches / Restart (캐시를 지우는 것)  
draft: false
---

## 안드로이드 R 에러
- file 의 Invalidate Caches / Restart (캐시를 지우는 것)  



## windowSoftInputMode 
- 키보드가 필요한 액티비티에 사용. 
- 매니패스트의 액티비티 태그에 android:windowSoftInputMode="" 로 사용
- "" 에 adjustPan 등을 입력. 종류가 다양함



## 안드로이드 해상도 별 크기 대응
[참고블로그](https://re-build.tistory.com/m/34)

- dimens.xml의 해상도 설정은 value폴더를 나뉘는 것으로 생성
- values-hdpi, values-xdpi 등 필요한 dpi 별 폴더를 res 폴더 아래에 생성하여 해당 폴더안에 dimens라는 이름으로 xml 파일 생성



## 안드로이드 해상도 별 크기 대응 2
- dimens 로 사용 시 같은 xxhdpi 를 사용하지만 화면의 크기가 다른 경우 발생. 
- 해당 경우는 activity 에서 직접 코드로 조건을 주게 됨
- DisplayMetrics 클래스를 이용
```java
 displayMetrics = activity.getResources().getDisplayMetrics();
        int deviceWidth = displayMetrics.widthPixels;
        int deviceHeight = displayMetrics.heightPixels;

        int setTopMargin = 68;

        if (deviceHeight < 2500 && deviceHeight > 2000) {
            ViewGroup.MarginLayoutParams iv_tmpimage = (ViewGroup.MarginLayoutParams) main_imageView.getLayoutParams();
            iv_tmpimage.setMargins(0, setTopMargin, 0, 0);
        } else if (deviceHeight <= 2000) {
             ViewGroup.MarginLayoutParams iv_tmpimage = (ViewGroup.MarginLayoutParams) main_imageView.getLayoutParams();
            iv_tmpimage.setMargins(0, (int) setTopMargin*0.5, 0, 0);
        }
```



## 키다운 이벤트 

```JAVA
    @Override
    public boolean onKeyDown(int keyCode, KeyEvent event) {
       if (event.getAction() == KeyEvent.ACTION_DOWN){
           if (keyCode == KeyEvent.KEYCODE_BACK){
               //registerUserFragment.replaceView();
           }

       }

        return super.onKeyDown(keyCode, event);
    }
```



## android life cycle onStop, onDestroy 

1. onStop 액티비티가 화면에서 완전히 사라질때. 즉 비활성 상태일때 호출.
	- 리소스와 상태정보를 유지하고 있는 상태
2. onDestroy는 액티비티의 종료 직전에 호출 되는데, finish() 가 실행되어야 콜백으로 호출된다.
	- finish()는 주로 사용자가 back key 를 눌렀을 때 호출이 된다. (Activity가 스스로 종료 하려고 하는 경우)
	- 안드로이드에서 시스템 메모리가 부족하여 강제로 Activitiy를 죽이는 경우에 호출할 수 있음.


