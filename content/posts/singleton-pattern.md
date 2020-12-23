---
title: "[디자인패턴] Singleton Pattern"
date: 2019-04-24T13:26:32+09:00
tags: ["DesignPattern","Singleton"]
keywords: ["디자인패턴","싱글톤패턴"]
description: "싱글톤 패턴이란 단 하나의 인스턴스만을 사용하는 패턴이다."
draft: false
---
- 싱글톤 패턴이란 단 하나의 인스턴스만을 사용하는 패턴이다.

### 예시
스피커의 볼륨을 조절하는 클래스의 인스턴스가 여러개라면 조절 할 때 마다 모든 인스턴스를 조절 해야하는 번거로움이 생긴다.<br>
그래서 하나의 인스턴스를 사용한다.<br>
하나의 인스턴스를 사용하기 위해 static으로 선언한다.
```
package Singleton;

public class SystemSpeaker {
    static private SystemSpeaker instance;
    private int volume;

    private SystemSpeaker() {
        volume = 5;
    }

    public static SystemSpeaker getInstance() {
        if (instance == null) {
            //시스템 스피커/ 아직 생성이 되지 않았을때는 생성을 해주고 
            instance = new SystemSpeaker();
        }
        //instance가 생성되어 있다면 그 인스턴스를 리턴한다.
        return instance;
    }

    public int getVolume() {
        return volume;
    }

    public void setVolume(int volume) {
        this.volume = volume;
    }
}
```
#### 메인 클래스<br>
같은 인스턴스를 사용하기 때문에 speaker1의 볼륨을 조절하던 speaker2의 볼륨을 조절하던 볼륨값은 둘다 바뀐다.
```
public class Main {
    public static void main(String[] args){
        SystemSpeaker speaker1 = SystemSpeaker.getInstance();
        SystemSpeaker speaker2 = SystemSpeaker.getInstance();

        System.out.println(speaker1.getVolume());
        System.out.println(speaker2.getVolume());

        speaker1.setVolume(10);

        System.out.println(speaker1.getVolume());
        System.out.println(speaker2.getVolume());

        speaker2.setVolume(13);

        System.out.println(speaker1.getVolume());
        System.out.println(speaker2.getVolume());

    }
}
```
#### 실행결과
![](/images/post/designpattern-singleton1.jpg)

<br>

### Reference
- [자바 디자인 패턴의 이해](https://youtu.be/5jgpu9-ywtY)