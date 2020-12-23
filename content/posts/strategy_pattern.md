---
title: "[디자인패턴] Strategy Pattern"
date: 2019-04-19T19:17:56+09:00
tags: ["DesignPattern", "Strategy"]
keywords: ["DesignPattern", "디자인패턴", "전략패텬", "strategy", "인터페이스","델리게이트"] 
description: "- 두 객체간의 연결을 해주는 장치
- 기능에 대한 선언과 구현의 분리
- 기능을 사용하는 통로"
draft: false
---

> 1. 인터페이스
> 2. 델리게이트
> 3. 스트래티지 패턴


## 인터페이스
---

- 두 객체간의 연결을 해주는 장치
- 기능에 대한 선언과 구현의 분리
- 기능을 사용하는 통로

```
public interface Ainterface {
    //기능의 선언
    public void funcA();
}
```

```
public class Aclass implements Ainterface {
    @Override
    public void funcA() { //기능의 구현
        System.out.println("AAA");
    }
}
```

```
public class Main {
    public static void main(String[] args){
        Ainterface ainterface = new Aclass();

        //a인터페이스를 사용할 수 있는 통로
        ainterface.funcA();
```

## 델리게이트
---

- 메소드의 역할을 위임한다
- 어떤 메소드의 처리를 다른 인스턴스의 메서드에 맡긴다

```
public class Aobj {

    Ainterface ainterface;

    public Aobj(){
        ainterface = new Aclass();
    }

    public void funcAA(){

        //위임
        ainterface.funcA();
        ainterface.funcA();
       // System.out.println("AAA");
       // System.out.println("AAA");

        //~기능이 필요합니다. 개발해주세요
    }
}
```

## 스트래티지 패턴
---

- 여러가지 알고리즘을 하나의 추상적인 접근점(인터페이스)을 만들어 접근점에서 서로 교환 가능하도록 하는 패턴

![](/images/post/designpattern_strategy1.png)


### 예제) 캐릭터와 무기 두종류(칼, 검)의 구현

무기 인터페이스
```
public interface Weapon {
    public void attack();
}
```
칼 클래스
```
public class Knife implements Weapon {
    @Override
    public void attack() {
        System.out.println("칼 공격");
    }
}
```

검 클래스
```
public class Sword implements Weapon {
    @Override
    public void attack() {
        System.out.println("검 공격");
    }
}
```
캐릭터 클래스
```
public class GameCharacter {
    //접근점(게임 캐릭터가 무기를 들고있음)
    private Weapon weapon;

    //교환기능(무기를 바꿀 수 있음)
    public void setWeapon(Weapon weapon) {
        this.weapon = weapon;
    }

    public void attack() {
        if(weapon == null){ //무기가 없을 시
            System.out.println("맨손 공격");
        }else{

            //델리게이트
            weapon.attack();
        }
    }
}
```
메인 메서드
```
public class Main {
    public static void main(String[] args){

        GameCharacter character = new GameCharacter();

        character.attack();

        character.setWeapon(new Knife());
        character.attack();

        character.setWeapon(new Sword());
        character.attack();
    }
}
```
새로운 무기 '도끼'의 추가
```
public class Ax implements Weapon {
    @Override
    public void attack() {
        System.out.println("도끼 공격");
    }
}
```
도끼클래스를 추가 생성하면 다른 것을 건들이지 않고 
메인에서 사용
```
 character.setWeapon(new Sword());
        character.attack();
```
<br />

### Reference
- [자바 디자인 패턴의 이해](https://youtu.be/UEjsbd3IZvA)
