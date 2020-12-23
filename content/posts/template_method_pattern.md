---
title: "[디자인패턴] Template Method Pattern"
date: 2019-04-22T19:05:14+09:00
tags: ["DesignPattern","Template Method"]
keywords: ["디자인패턴","템플릿메서드"]
description: "- 알고리즘의 구조를 메서드에 정의하고 하위 클래스에서 알고리즘의 구조의 변경 없이 알고리즘을 재정의 하는 패턴 - 구현하려는 알고리즘이 일정한 프로세스가 있다 - 구현하려는 알고리즘이 변경 가능성이 있다"
draft: false
---

- 알고리즘의 구조를 메서드에 정의하고 하위 클래스에서 알고리즘의 구조의 변경 없이 알고리즘을 재정의 하는 패턴
  - 구현하려는 알고리즘이 일정한 프로세스가 있다
  - 구현하려는 알고리즘이 변경 가능성이 있다

## 템플릿 메서드 기본 설계구조
---

![](/images/post/designpattern_templatemethod1.png)

## 템플릿 메서드 패턴의 구현 단계
---

1. 요구사항에 대한 알고리즘을 여러 단계로 나눈다
2. 나눠진 알고리즘의 단계를 메서드로 선언한다
3. 알고리즘을 수행할 템플릿 메서드를 만든다
4. 하위 클래스에서 나눠진 메서드들을 구현한다

## 예제

신작 게임의 접속을 구현해주세요

- requestConnection(String str): String

유저가 게임 접속시 다음을 고려해야 합니다

- 보안 과정 : 보안 관련 부분을 처리합니다
  - doSecurity(String string):String
- 인증 과정 : user name과 password가 일치하는지 확인합니다
  - authentication(String id, String password):boolean
- 권한 과정 : 접속자가 유료 회원인지 무료 회원인지 게임 마스터 인지 확인합니다
  - authorization(String userName):int
- 접속 과정 : 접속자에게 커넥션 정보를 넘겨줍니다
  - connection(String info):String

현재 위의 요구 사항에서 이미  단계가 나눠져 있고 메서드가 정해져 있다.<br>

추상 클래스

```
package Template_Method.helperPkg;

public abstract class AbstGameConnectHelper {
    //알고리즘의 단계라서 외부(패키지)에 노출이 되면안되지만 하위 클래스에선 사용할 수 있어야 함 -> protected 접근 제어자 사용
    protected abstract String doSecurity(String string);

    protected abstract boolean authentication(String id, String password);

    protected abstract int authorization(String userName);

    protected abstract String connection(String info);

    //템플릿 메서드
    public String reqeustConnection(String str) {
        //보안 작업 -> 암호화 된 문자열을 복호화
        String decodedInfo = doSecurity(str);
        //반환 된 것을 가지고 아이디, 암호를 할당.
        String id = "aaa";
        String password = "bbb";

        if (!authentication(id, password)) {
            throw new Error("아이디 암호 불일치");
        }

        String userName = "";
        int i = authorization(userName);

        switch (i) {
            case -1: //셧다운을 적용할 때 권한 확인에서 -1를 리턴 시
                throw  new Error("셧다운");
            case 0: // 게임 매니저
                break;
            case 1: // 유료 회원
                break;
            case 2: // 무료 회원
                break;
            case 3: // 권한 없음
                break;
            default: // 기타 상황
                break;
        }


        return connection(decodedInfo);
    }
}
```

추상메서드의 구현 클래스

```
package Template_Method.helperPkg;

public class DefaultGameConnectionHelper extends AbstGameConnectHelper {
    @Override
    protected String doSecurity(String string) {
        System.out.println("강화된 알고리즘을 이용한 디코드");
        return string;
    }

    @Override
    protected boolean authentication(String id, String password) {
        System.out.println("아이디/암호 확인 과정");
        return true;
    }

    @Override
    protected int authorization(String userName) {
        System.out.println("권한 확인");
        //서버에서 유저이름 유저의 나이를 알 수 있다.
        //나이를 확인하고 시간을 확인하고 미성년자일때 10시가 지났다면
        //권한이 없는 것으로 한다.
        return 0;
    }

    @Override
    protected String connection(String info) {
        System.out.println("접속 단계");
        return info;
    }
}
```

Main 클래스

```
package Template_Method;

import Template_Method.helperPkg.AbstGameConnectHelper;
import Template_Method.helperPkg.DefaultGameConnectionHelper;

public class Main {
    public static void main(String[] args){
        AbstGameConnectHelper helper = new DefaultGameConnectionHelper();

        helper.reqeustConnection("아이디 암호 등 접속 정보");
    }
}
```

![](/images/post/designpattern_templatemethod2.png)
패키지를 분리하여 helper 변수에 추상메서드들이 나타나지 않는 것을 확인할 수 있다.

실행 결과

![](/images/post/designpattern_templatemethod3.png)

<br>

### Reference

- [자바 디자인 패턴의 이해](<https://youtu.be/qr7I18Lhsl8>)