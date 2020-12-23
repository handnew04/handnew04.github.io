---
title: "[Android] permission"
date: 2019-12-25T22:35:44+09:00
tags: ["permission", "권한", "Android"]
keywords: ["안드로이드 권한", "Android", "permission"]
description: "안드로이드 23 이상에서의 권한 요청  
매니패스트에 선언한 권한목록을 가져올 수 있다."
draft: false
---

안드로이드 23 이상에서의 권한 요청  
매니패스트에 선언한 권한목록을 가져올 수 있다.  
String\[\] 의 형태로 받을 수 있다.

```
 try {
       String[] permissionList = context
                    .getPackageManager()
                    .getPackageInfo(context.getPackageName(), PackageManager.GET_PERMISSIONS)
                    .requestedPermissions;
} catch (PackageManager.NameNotFoundException e) {
            //throw new RuntimeException ("Exception", e);
}
```

권한 목록중 허가되지 않은 권한을 확인하고

```
public static String[] checkPermissions(Context context, String[] permissionList) {
        ArrayList<String> requestList = new ArrayList<>();
        for (String aPermission : permissionList) {
            int permissionCheck = ContextCompat.checkSelfPermission(context, aPermission);
            if (permissionCheck == PackageManager.PERMISSION_DENIED) {
                requestList.add(aPermission);
            }
        }
        return requestList.toArray(new String[requestList.size()]);
    }
```

권한 요청을 띄운다

```
 ActivityCompat.requestPermissions(mActivity, String["요청할 권한 목록"], 100);
```

콜백 메서드에서 권한 요청 후의 처리를 한다.

```
@Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        //super.onRequestPermissionsResult(requestCode, permissions, grantResults);
            if (requestCode == 100) {
/*requestCode : 권한 요청시 보냈던 리퀘스트 코드
permissions : 권한허가 요청 한 권한 리스트
grantResults : 권한 허가 결과 리스트 (permission[0]의 결과 grantResult[0])*/
                } 
            }
    }
```