# Object

Object는 모든 클래스의 조상이라고 할 수 있다
모든 클래스가 공통으로 포함하고 있어야 하는 기능을 제공해준다.

Object의 기능들을 하나씩 살펴보도록 하자

#### toString
---
```java
Calculator c1 = new Calculator();
```
`sysout(c1)` 의 출력물은 다음과 같다.
=>`org.opentutorials.javatutorials.progenitor.Calculator@11be650f`

Calculator 클래스의 어떠한 값이다~ 라고 적혀있는데 

`sysout(c1.toString())` 의 출력물도 위와 같은 결과물이 나온다.

이 말이 뜻하는 것은 c1을 출력하면, JAVA에서 Object의 `toString` 메서드를 자동으로 불러와 실행시킨다는 것


#### equals
객체와 객체가 같은 것인지 비교한다.
이 메서드를 오버라이딩하겠다.
객체끼리 비교할 때는 이 메서드를 만들기를 권고한다.

```java
class Student{
  String name;
  public boolean equals(Object obj){
    Student _obj = (Student)obj;
    return this.name == _obj.name
  }
}
```
`Student _obj = (Student)obj;` 
obj는 Object이기 때문에 부모 클래스이다.
부모 클래스를 Student 클래스에 대입하기 위해서는 명시적으로 적어주는 방법을 이용해야 한다. 

#### finalize
객체가 소멸될 때 호출되기로 약속하는 메소드
자바에서는 이 메서드를 안쓰길 권고하는데 자동으로 해주기 때문이다 
이것을 `가비지 컬렉션` 이라고 한다.

> 가비지 컬렉션 
인스턴스를 만다는 것은 컴퓨터의 메모리를 이용한다 (RAM)
이 램을 효율적이게 사용하기 위해서 데이터를 램에서 제거할 수 있는 방법들을 제공한다.
어떤 인스턴스를 만들었다가 사용하는 곳이 더이상 없다면 변수와 변수에 담겨있는 인스턴스는 메모리에서 삭제한다. 


#### clone

어떤 객체를 복제해주는 기능이다.

`s1.clone()` 으로 복제를 하려고 한다 

```java
class Student implements Cloneable{
    String name;
    Student(String name){
        this.name = name;
    }
    protected Object clone() throws CloneNotSupportedException{
        return super.clone();
    }
}
 
class ObjectDemo {
 
    public static void main(String[] args) {
        Student s1 = new Student("egoing");
        try {
            Student s2 = (Student)s1.clone();
            System.out.println(s1.name);
            System.out.println(s2.name);
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
 
}
```

1. `Cloneable` 이 적혀 져 있어야 `s1.clone()` 으로 사용이 가능해진다.
2. clone 메서드는 Object 클래스에서 protected이기 때문에 같은 패키지가 아닐때 사용이 불가능하다
  -> 오버라이딩
3. 오버라이딩을 하려고 하면, clone()에서 예외 처리가 필수적이라는 오류가 나온다. 
  - runtimeException 이 아닌 Exception을 상속받기 때문
4. 메서드를 사용하기 위해 try, catch 를 사용하며, 명시적으로 클래스를 Student로 바꿔줘야 한다.
  `Student s2 = (Student)s1.clone();`


# 상수 

상수는 변하지 않는 값이다. 

예시를 통해 알아보자 

```java
    private final static int APPLE = 1;

```

#### final 
변수에 final로 처리하면 한번 설정된 값은 더이상 바뀌지 않는다.

#### static 
클래스 변수
바뀌지 않는 값이라면 인스턴스 변수가 아닌 클래스 변수라는 의미로 적어주면 좋다.

## enum
- enumerated : 열거형이라는 뜻이다.
- ***열거형은 서로 연관된 상수들의 집합***이다. 


```java
enum Fruit{
    APPLE, PEACH, BANANA;
}

Fruit type = Fruit.APPLE;
switch(type){
    case APPLE:
        System.out.println(57+" kcal");
        break;
    case PEACH:
        System.out.println(34+" kcal");
        break;
    case BANANA:
        System.out.println(93+" kcal");
        break;
}

```
서로 연관되어 있는 상수들의 집합이기 때문에 switch 문에서 편리하게 사용가능하다.


enum은 사실상 class이다. 증명해보자 
```java
enum Fruit{
    APPLE, PEACH, BANANA;
    Fruit(){
      sysout("hi")
    }
}
=> hi hi hi
```

그렇다 저 상수값이 등록될 때마다 `public static final Fruit APPLE = new Fruit();` 라는 생성자가 실행되고 있었던 것이다.

열거형 내부에 생성자, 필드, 메소드를 가질 수 있기 때문에 단순히 상수로만 사용하는 것이 아닌 더 많은 역할이 가능하다.

```java
for (Fruit f:Fruit.values()){
  sysout(f);
}
```
