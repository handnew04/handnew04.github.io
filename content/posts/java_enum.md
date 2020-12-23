---
title: "[JAVA] enum type"
date: 2019-08-13T22:05:18+09:00
tags: ["java","enum","singleton"]
keywords: []
description: "열거 자료형
기존의 java 에서 상수를 사용할 때 아래와 같이 정의한다."
draft: false
---

- 열거 자료형

기존의 java 에서 상수를 사용할 때 아래와 같이 정의한다.

```
//과일
public static int F_APPLE = 1;
public static int F_MANGO = 2;
public static int F_MELON = 3;

//의류
public static int C_ZARA = 1;
public static int C_MANGO = 2;
public static int C_SPAO = 3;
```
위의 코드에서 2와 비교를 할 때 과일과 의류의 MANGO 는 따로 정의 되어 있지만 비교시에 둘 다 2로써 값이 같다고 여기게 된다.
과일 타입을 받는 메서드가 있다고 할 때, 의류 변수를 넣어도 동작하게 될 것이다.
이런 경우 enum을 사용하여 구분을 쉽게 할 수 있다.
아래 처럼 enum을 사용하여 열거 할 수 있다.
```
public enum Fruits {APPLE, MANGO, MELON}
public enum Clothes {ZARA, MANGO, SPAO}
```
이것은 실제로 아래의 코드와 동일하다
```
public class Fruits {
public static int APPLE = new Fruits();
public static int MANGO = new Fruits();
public static int MELON = new Fruits();
}
```
앞에서부터 0, 1, 2 의 값을 가진다.

enum은 생성자가 private로 외부에서 인스턴스화를 할 수가 없다. 
내부에서 생성자를 사용하는 방식
```
public enum Fruits {
    APPLE(1000);
    MANGO(2000);
    MELON(3000);

    final private int number;

    private Fruits(int number){
    this.number = number;
    }
}
```
getter 메서드를 생성하여 해당 내용을 가져올 수 있다.

enum은 클래스처럼 사용하기에 내부에 상수열거 뿐 아니라 일반 변수 및 메서드를 사용할 수 있다. 

## enum 의 singleton pattern
```
public enum Sample {
INSTANCE;

int NUMBER_MAX = 100;
int NUMBER_MIN = 10;
}
```
처음 코드를 보았을 때 이해가 되지 않았다. enum 클래스 안의 떡하니 있는 INSTANCE.
위의 enum type 인 것이다. APPLE, MANGO 처럼 
사실은 아래 코드와 같다.
```
public enum Sample {
public static int INSTANCE = new Sample();
}
```
하나의 인스턴스만을 사용하는 싱글톤패턴을 잘 보여주고 있다. 
외부 클래스 등에서 
```
int nMax = Sample.INSTANCE.getInt("NUMBER_MAX");
```
로 사용 할 수 있다.
물론 getInt 메서드는 따로 enum 클래스 내부에 만들어 두어야 한다.

자료형 타입에 따라 다른 getDouble, getInt, get(배열 등) 등으로 만들어두면 여러타입의 상수가 있을 때 용의하다.