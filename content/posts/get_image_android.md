---
title: "[Android] 이미지 가져오기 (촬영, 내부저장소, 자르기) "
date: 2020-07-12T00:39:08+09:00
tags: ["android","image","camera","provider"]
keywords: ["android", "image", "camera", "안드로이드 이미지", "안드로이드 이미지 크롭"]
description: "return-data 를 이용 하여 intent 로 크롭된 이미지가 넘어오도록 함"
draft: false
---

## 지정된 비율로 리사이즈 크롭

return-data 를 이용 하여 intent 로 크롭된 이미지가 넘어오도록 함

```
 @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);

        if (resultCode != RESULT_OK) return;

        switch (requestCode) {
            case PICK_FROM_ALBUM:
                Uri photoUri = data.getData();
                cropImage(photoUri);
                    break;
            case PICK_FROM_CAMERA:
                    break;
            case CROP_FROM_IMAGE:
                Bundle bundle = data.getExtras();
                assert bundle != null;
                Bitmap test = bundle.getParcelable("data");            
                    break;
        }
    }

  private void cropImage(Uri imageUri) {
        Intent intent= getCropIntent(imageUri);
        startActivityForResult(intent, CROP_FROM_IMAGE);
    }

    private Intent getCropIntent(Uri inputUri) {
        Intent intent = new                      Intent("com.android.camera.action.CROP");
        intent.setFlags(Intent.FLAG_GRANT_WRITE_URI_PERMISSION);
        intent.setFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);

        intent.setDataAndType(inputUri, "image/*");

        intent.putExtra("aspectX", 4);
        intent.putExtra("aspectY", 3);
        intent.putExtra("outputX", 400);
        intent.putExtra("outputY", 300);
        intent.putExtra("scale", true);

        //intent.putExtra(MediaStore.EXTRA_OUTPUT, outputUri);
        intent.putExtra("return-data", true);

        return intent;
    }
```

## 이미지 비율 유지하며 리사이즈(크롭 x)

```
private Bitmap resize(Context context, Uri uri, int resize) {
        Bitmap resizeBitmap = null;

        BitmapFactory.Options options = new BitmapFactory.Options();
        try {
            BitmapFactory.decodeStream(context.getContentResolver().openInputStream(uri), null, options); // 이미지의 크기를 options 에 담아줌

            int width = options.outWidth;
            int height = options.outHeight;
            int samplesize = 1; // 숫자가 클수록 용량이 작아짐, 4 라고 하면 4픽셀을 1픽셀로 만들어줌

            while (true) { //가로세로 크기를 리사이즈크기에 최대한 맞춰서 작을때까지 반복함.
                if (width / 2 < resize || height / 2 < resize)
                    break;
                width /= 2;
                height /= 2;
                samplesize *= 2;
            }

            options.inSampleSize = samplesize;
            Bitmap bitmap = BitmapFactory.decodeStream(context.getContentResolver().openInputStream(uri), null, options); //정해진 샘플사이즈로 비트맵을 다시만든다
            resizeBitmap = bitmap;

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        return resizeBitmap;
    }
```

## 내부저장소 이미지 저장

```
private File createFIle() {
        String fileName = "profileSample";
        File imageDir = getApplicationContext().getDir("profileImages", MODE_PRIVATE);
        return new File (imageDir, fileName+".png");
    }

    private void saveImageFile(Bitmap profileImage) {
        // 중복 제거
        boolean deleted = profileImagePath.delete();
        Log.w(TAG, "Profile Delete Check : "+ deleted);
        FileOutputStream fosImage = null;

        try {
            fosImage = new FileOutputStream(imagePath);
            profileImage.compress(Bitmap.CompressFormat.PNG,100,fosImage);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } finally {
            try {
                assert fosImage != null;
                fosImage.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```

## 카메라 사진 가져오기

퍼미션 추가

```
  <uses-permission android:name="android.permission.CAMERA"/>
```

카메라 켜기

-   provider 없이(저장경로 없이) 촬영 하게 되면 촬영된 이미지가 아닌 이미지의 썸네일이 넘어오게 되어 아주 작은 이미지를 볼 수 있다.
-   찍은 사진이 저장될 경로를 같이 보내주어야 하는데 위의 앨범이미지 가져올 때 사용한 File path 는 file:// 로 시작한다. 안드로이드 정책상 외부 앱으로 file:// - 주소를 보낼 수 없음
-   file:// -> content:// 주소로 변경해주어야 함. 이때 provider 필요
-   FileProvider 가 해당 file path에서 content:// 주소를 만들어준다.

path를 적은 xml 파일 필요

```
<?xml version="1.0" encoding="utf-8"?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
 <external-path name="profilePath" path="."/>
 <root-path name ="root" path ="."/>
</paths>
```

매니패스트 등록

```
   <provider
            android:authorities="프로젝트 패키지 명"
            android:name="android.support.v4.content.FileProvider"
            android:exported="false"
            android:grantUriPermissions="true">
            <meta-data
                android:name="android.support.FILE_PROVIDER_PATHS"
                android:resource="@xml/위의 xml파일명"/>
        </provider>
```

카메라 실행

```
       Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
                File photoFile = createFIle();
                Uri providerFileUri = FileProvider.getUriForFile(getApplicationContext(), getPackageName(), photoFile);
                intent.putExtra(MediaStore.EXTRA_OUTPUT, providerFileUri);
                startActivityForResult(intent, PICK_FROM_CAMERA);
```

해당 경로(data/data/앱패키지명/지정파일명/파일)에 파일이 저장되는 것을 확인할 수 있다.