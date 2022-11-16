---
weight: 1
title: "람다식"
---

# 람다식 Lambda Expression

<span hidden>794 ~ 800p</span>

---

## 람다식

> Java 8 부터 제공되는 메서드를 하나의 식으로 표현하는 기능

람다식을 사용하면 메서드의 이름과 반환값이 없어지므로 `익명함수 Anonymous Function` 라고 부르기도 한다.

람다식의 사용방법을 예제로 살펴보자.

**람다식 X**

```java
int[] arr = new int[5];
Arrays.setAll(arr, method());

int method() {
    return (int) (Math.random() * 5) + 1;
}
```

**람다식 O**

```java
int[] arr = new int[5];
Arrays.setAll(arr, (i) -> (int)(Math.random() * 5) + 1);
```

위와 같이 람다식을 사용하면 따로 메서드를 `선언-정의-호출`해 줄 필요가 없다.

### 규칙1. 매개변수 타입을 추론 가능할 경우 생략할 수 있다.

```java
(int a, int b) -> a > b ? a : b
```

```java
(a, b) -> a > b ? a : b
```

### 규칙2. 표현식이 하나일 경우 대괄호는 생략할 수 있다.

```java
(String name, int i) -> {
    System.out.println(name + "=" + i);
}
```

```java
(String name, int i) -> System.out.println(name + "=" + i)
```

---

## 함수형 인터페이스

자바에서 모든 메서드는 클래스 내에 포함돼야 한다.

람다식은 어떤 클래스에 포함돼있을까?

사실 람다식은 메서드와 동등하지 않고, 익명 클래스의 객체와 동등하다.

```java
(int a, int b) -> a > b ? a : b
```

```java
new Object() {
    int max(int a, int b) {
        return a > b ? a : b;
    }
}

// max() 메서드는 임의의 메서드로 큰 의미는 없다.
```

그렇다면 만약 해당 객체를 임의의 참조변수에 저장한다면 어떻게 될까?

```java
타입 temp = (int a, int b) -> a > b ? a : b;
```

예를 들어, MyFunction 이라는 인터페이스가 정의돼 있다.

```java
Interface MyFunction {
    public abstract int max(int a, int b);
}
```

이 인터페이스를 구현한 익명 클래스는 다음과 같이 생성해서 사용가능하다.

```java
MyFunction temp = new MyFunction() {
    @Override
    public int max(int a, int b) {
        return a > b ? a : b;
    }
};

int num = temp.max(5, 3);
```

람다식이 어떤 방식으로 구현되고 있는지 이해가 되는가?

하나의 인터페이스에 하나의 추상메서드를 정의해 람다식을 구현하는 방식은 자바의 규칙을 어기지 않는다.

이렇게 람다식을 다루기 위한 인터페이스를 `함수형 인터페이스 Functional Interface` 라고 부른다.

```java
@FunctionalInterface
interface MyFunction {
    public abstract int max(int a, int b);
}
```

### 규칙1. 하나의 인터페이스에 하나의 추상메서드만 정의 가능하다.

> 함수형 인터페이스의 경우 하나의 인터페이스에 하나의 추상메서드만이 정의될 수 있다.

그래야 람다식과 인터페이스가 1대1 로 매핑될 수 있기 때문이다.

### 규칙2. static 메서드와 default 메서드의 개수에는 제약이 없다.

> static 과 default 키워드가 붙은 메서드의 개수에는 제약이 없다.

## 핵심 정리

> 핵심은 메서드를 주고 받는 것이 아니라 `함수형 인터페이스를 구현한 익명 객체`를 주고 받는다는 것이다.

```java
@FunctionalInterface
interface MyFunction {
    void run();
}

class LamdaEx {
    static void excute(MyFunction f) {
        f.run();
    }

    static MyFunction getMyFunction() {
        MyFunction f = new MyFunction() {
            @Override
            public void run() {
                System.out.println("MyFunction run");
            }
        };

        return f;
    }

    static MyFunction getMyFunctionLamda() {
        MyFunction f = () -> System.out.println("MyFunction Lamda run");
        return f;
    }

    public static void main(String[] args) {

        MyFunction f1 = getMyFunction();
        MyFunction f2 = getMyFunctionLamda();

        f1.run();
        f2.run();
        excute(f1);
    }
}
```

```
MyFunction run
MyFunction Lamda run
MyFunction run
```
