---
title: "[Android] 스피너 (Spinner)"
date: 2020-07-26T17:50:32+09:00
tags: ["Android","Spinner"]
keywords: ["Android", "Spinner", "스피너"]
description: "ArrayAdapter 의 context 자리에 activity 는 가능하나 fragment에서 사용할 경우 getActivity 를 가져와야 함"
draft: false
---

## 동적 스피너

ArrayAdapter 의 context 자리에 activity 는 가능하나 fragment에서 사용할 경우 getActivity 를 가져와야 함

```
 private void initSpinner() {
        List<String> years = getYears();
        ArrayAdapter<String> adapter = new ArrayAdapter<>(this, android.R.layout.simple_spinner_dropdown_item, years);
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        yearsSpinner.setAdapter(mModelYearsAdapter);
    }

    private List<String> getYears() {
        int currentYear = Calendar.getInstance().get(Calendar.YEAR);
        int minYear = 2000;
        List<String> years = new ArrayList<>();

        while (currentYear >= minModelYear) {
            years.add(String.valueOf(currentYear));
            currentYear--;
        }

        return years;
    }
```

## 커스텀 스피너 레이아웃 (스피너의 디자인을 통일 할 때
(본인이 원하는 형태의 디자인) layouy/spinner\_xxx.xml 을 추가한 뒤

```
<?xml version="1.0" encoding="utf-8"?>
<TextView style="@style/FontTheme12sp"
    android:layout_width="match_parent"
    android:layout_height="40dp"
    android:gravity="center_vertical"
    android:paddingStart="12dp"
    android:paddingEnd="12dp"
    android:textColorHint="@color/colorPrimary"
    xmlns:android="http://schemas.android.com/apk/res/android" />
```

-   Activity 에 아래 ArrayAdapter 의 layout 부분에 해당 xml 을 추가
-   setDropDownViewResource에 기본 simple\_spinner\_dropdown 을 추가하면 드롭다운의 뷰는 기본으로 설정된다. 지우거나 다른 뷰를 설정할 경우 해당 xml 의 디자인을 따르게 됨

```
    ArrayAdapter<String> adapter = new ArrayAdapter<>(activity, R.layout.spinner_xxx, getResources().getStringArray(R.array.xxxArray));
          adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
          xxxSpinner.setAdapter(adapter);
```

## 커스텀 스피너 레이아웃 추가 (개별적 커스텀이 필요할 경우)

```
private OnItemSelectedListener exSpinner = new AdapterView.OnItemSelectedListener() {
    public void onItemSelected(AdapterView<?> parent, View view, int pos, long id) {

       ((TextView) parent.getChildAt(0)).setTextColor(Color.RED);
       ((TextView) parent.getChildAt(0)).setTextSize(12);
        //외 padding 등 추가 
    }

    public void onNothingSelected(AdapterView<?> parent) {

    }
};
```