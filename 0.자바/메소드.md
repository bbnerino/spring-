메소드는 코드를 재사용할 수 있게 한다.

> 지금껏 자바를 사용하면서 아래와 같은 걸 많이 봤을 것이다. 이게 메소드다

```java
public static void main(String[] args){
	return
}
```

## 메소드 정의 / 호출
define / call

```java
public class Number {

  public static void numbering() {
    int i = 0;
    while (i < 10) {
      i++;
      System.out.println(i);
    }
  }

  public static void main(String[] args) {
    numbering();
  }
}
```

`numbering` 이라는 메소드를 정의하고 호출했다.

`numbering()` 으로 괄호로 마무리하면 호출하는 것이고
`numbering(){정의}` 괄호 뒤에 중괄호 안에서는 정의를 한다.


> main 메소드가 무엇일까 ?  규칙이다
우리가 만드는 프로그램은 반드시 public static void main(String[] args)가 이끄는 중괄호 안에서 적어야 한다. 그렇게 코드를 작성하면 자바는 main메소드를 실행하는 것이다. 
=> main 메소드를 우리가 정의를 하는것이고, 자바는 실행을 하는 것이다.



## 매개변수와 인자 
```java
  public static void numbering(int limit) {
    int i = 0;
    while (i < limit) {
      i++;
      System.out.println(i);
    }
  }

  public static void main(String[] args) {
    numbering(10);
  }
```

## void

void 가 메소드 앞에 붙으면 결과값이 존재하지 않는 것이다.

함수에 return 을 적고 싶다면 void를 빼고 작성해야한다.

> 함수안에서 처리하지 않고  return 하는 것이 좋은 이유?
부품으로서의 가치를 높이기 위해서 이다. 각자 다른 목적으로 하나의 메서드를 사용할 수 있게 된다.
