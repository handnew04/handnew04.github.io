---
title: "[Notion] 오늘이 지나면 자동으로 x 체크 되는 함수"
date: 2020-12-24T00:01:58+09:00
tags: ["Notion"]
keywords: ["Notion", "Auto Checked"]
description: "노션의 달력에서 매일 할일을 기록하고 오늘이 지났을때 완료 표시가 없으면 자동으로 x를 완료 체크를 하면 체크표시가 나오도록 하고싶었다."
draft: false
---
노션의 달력에서 매일 할일을 기록하고 오늘이 지났을때 완료 표시가 없으면 자동으로 x를 완료 체크를 하면 체크표시가 나오도록 하고싶었다.
![](/images/post/2020_12_23_img1.png)

오늘과 이후의 할 일에 대해선 완료 표시가 없어도 x가 표시되지 않는다. 
하지만 오늘 이전의 할 일들은 완료한 것에 대해선 체크가, 완료하지 않은 것에 대해선 x 가 표시 된다. 

![](/images/post/2020_12_23_img2.png)
체크가 없는 할일

![](/images/post/2020_12_23_img3.png)
체크를 할시
```
if(and(prop("Date") < now(), prop("Done") == true), format("✅☑✅"), 
if(dateBetween(prop("Date"), now(), "days") < 0, format("❌"), ""))
```