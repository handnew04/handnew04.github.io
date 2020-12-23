---
title: "[Android] AWS S3 이미지 업로드"
date: 2020-07-12T01:22:44+09:00
tags: ["Aws", "S3", "Android"]
keywords: ["Aws", "Android" , "S3", "S3 이미지 업로드"]
description: "1.  AWS IAM 에서 ACCESS KEY, SECRET KEY 얻기 2.  S3 에서 BUCKET 및 아래 폴더 생성 3.  안드로이드 gradle 추가"
draft: false
---

> 1.  AWS IAM 에서 ACCESS KEY, SECRET KEY 얻기
> 2.  S3 에서 BUCKET 및 아래 폴더 생성
> 3.  안드로이드 gradle 추가
> 4.  매니패스트 서비스 추가
> 5.  코드 작성

## 1\. AWS IAM 에서 ACCESS KEY, SECRET KEY 얻기

우선 AWS 의 IAM 콘솔 - 사용자에 추가하여 액새스키와 시크릿키를 얻는다.  
시크릿키는 만들 때 한번만 보여주기 때문에 잊어버리면 사용자를 다시 추가하여야 한다.

## 2\. S3 에서 BUCKET 및 아래 폴더 생성

버킷을 생성하고 버킷 내부에 파일을 저장할 폴더 생성

## 3\. 안드로이드 gradle 추가

app gragle 에 추가 (버전은 최신을 찾아 볼 것)

```
implementation 'com.amazonaws:aws-android-sdk-cognito:2.13.5' 
implementation 'com.amazonaws:aws-android-sdk-s3:2.13.5'
implementation 'com.amazonaws:aws-android-sdk-mobile-client:2.13.5'
```

## 4\. 매니패스트 서비스 추가

```
    <service android:name="com.amazonaws.mobileconnectors.s3.transferutility.TransferService"  
    android:enabled="true" />
```

## 5\. 업로드 코드작성

Region.getRegion 은 지역인데 , AP\_NORTHEAST\_2 가 서울.

```
AWSCredentials awsCredentials = new BasicAWSCredentials(accessKey, secretKey);
AmazonS3Client s3Client = new AmazonS3Client(awsCredentials, Region.getRegion(Regions.AP_NORTHEAST_2));

TransferUtility transferUtility = TransferUtility.builder().s3Client(s3Client).context(this).build();
TransferNetworkLossHandler.getInstance(this);

TransferObserver uploadObserver = transferUtility.upload(bucketName, folder+fileName, file);
uploadObserver.setTransferListener(new TransferListener() {
            @Override
            public void onStateChanged(int id, TransferState state) {
                Log.d(TAG, "onStateChanged: " + id + ", " + state.toString());

            }

            @Override
            public void onProgressChanged(int id, long bytesCurrent, long bytesTotal) {
                float percentDonef = ((float) bytesCurrent / (float) bytesTotal) * 100;
                int percentDone = (int)percentDonef;
                Log.d(TAG, "ID:" + id + " bytesCurrent: " + bytesCurrent + " bytesTotal: " + bytesTotal + " " + percentDone + "%");
            }

            @Override
            public void onError(int id, Exception ex) {
                Log.e(TAG, ex.getMessage());
            }
     });
```

-   file 확장자
    
    ```
    String fileExtension = fileAbsolutePath.substring(fileAbsolutePath.lastIndexOf(".")+1);
    ```
    

## 6\. 다운로드 코드작성

업로드와 위의 코드는 동일 하며 TransferObserver 의 메서드만 다르게 사용

```
 TransferObserver downloadObserver = transferUtility.download(bucketName,uploadPath, filePath);
            downloadObserver.setTransferListener(new TransferListener() {
                @Override
                public void onStateChanged(int id, TransferState state) {
                    if (state == TransferState.COMPLETED) {
                        // 저장 완료
                    }
                }

                @Override
                public void onProgressChanged(int id, long bytesCurrent, long bytesTotal) {

                }

                @Override
                public void onError(int id, Exception ex) {

                }
            });
        }
```