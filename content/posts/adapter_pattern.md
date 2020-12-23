---
title: "[디자인패턴] Adapter Pattern"
date: 2019-04-21T16:11:26+09:00
tags: ["DesignPattern","adapter"]
keywords: ["어댑터패턴","디자인패턴"]
draft: false
description: 기계, 기구 등을 다목적으로 사용하기 위한 부가기구 - 전기 110v 코드를 220v 로 바꿔주는 것 또한 어댑터
---

## Adapter란?
---
- 기계, 기구 등을 다목적으로 사용하기 위한 부가기구<br>
- 전기 110v 코드를 220v 로 바꿔주는 것 또한 어댑터<br>

코드에서도 마찬가지로 사용처에 맞게 변환을 해주는 역할을 한다.

Math 라는 클래스가 있고 메서드는 double로 값을 받고 리턴값도 double 로 내보낸다.
```
public class Math {
    public static double twoTime(double num) {
        return num * 2;
    }

    public static double half(double num) {
        return num / 2;
    }
}
```
adapter 인터페이스
```
public interface Adapter {

    //원하는 기능
    public Float twiceOf(Float f);
    public Float halfOf(Float f);

}
```
어댑터 인터페이스를 구현할 클래스<br>
double로 매개변수와 리턴값을 가진 twoTime 메서드를 float타입으로 사용할 수 있게 코드를 작성
```
public class AdapterImpl implements Adapter {

    @Override
    public Float twiceOf(Float f) {
        return (float) Math.twoTime(f.doubleValue());
         // return Math.twoTime(f.doubleValue()).floatValue();
    }

    @Override
    public Float halfOf(Float f) {
        return (float)Math.half(f.doubleValue());
    }
}
```
메인 클래스<br>
어댑터 인터페이스를 통해 double이 아닌 float 타입 사용 가능
```
public class Main {
    public static void main(String[] args) {
        Adapter adapter = new AdapterImpl();

        System.out.println(adapter.twiceOf(100f));
        System.out.println(adapter.halfOf(80f));

    }
}
```
만약 halfOf 메서드를 사용할 때 출력문을 추가해야 한다면, Math 클래스의 메서드에 직접 추가시 Math를 사용하는 모든 코드에서 출력문이 추가되는 사태 발생<br>
그래서 인터페이스를 구현한 클래스 AdapterImpl의 메서드에 추가<br>
```
  @Override
    public Float halfOf(Float f) {
        System.out.println("절반 함수 호출");
        return (float)Math.half(f.doubleValue());
    }
```
<br>

### Reference
- [자바 디자인 패턴의 이해](https://youtu.be/gJDZ7pcvlAU)