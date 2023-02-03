# 예외처리 (Exception)
---

```java
class Calculator{
  int left,right;
  public void Calculator(int left, int right){
    this.left = left;
    this.right = right;
  }
  public void divide(){
    sysout(this.left/this.right)
  }
}

```

```java
Calculator c1 = Calculator(10,0);
c1.divide(); => 에러
```

0으로 나누게 되면 산술 에러가 나오게 된다.
이 코드를 이제 예외처리를 통해 에러출력이 나오지 않게 하는법을 알아보자

### try / catch

```java
  public void divide(){
    try{
      sysout("결과는... ㄷㄱㄷㄱ")
      sysout(this.left/this.right)
    }
    catch(Exception e){
      sysout("오류가 발생하였습니다." + e.getMessage());
    }
    sysout("끝")
  }
```

```java
  c1.divide(); =>  "결과는... ㄷㄱㄷㄱ 오류가 발생했습니다 : by Zero 끝"
```

try 안에 "결과는 ... ㄷㄱㄷㄱ" 까지 출력되고 그 뒤에는 오류로 인해 catch로 이동했다.

- `try{L}` L: 예외의 발생이 예상되는 로직
- `catch(예외클래스 인스턴스){L}` L: 예외가 발생했을 때 실행되는 로직

### 예외클래스 인스턴스

`Exception e`

- `e.getMessage()` => / by zero

  - 간단한 형태의 에러 메시지

- `e.toString()` => /java.lang.ArithemeticException / by zero

  - 더 자세한 예외 정보를 제공
  - 발생한 예외가 어떤 예외에 해당하는지에 대한 정보

- `e.printStackTrace()`
  - 이 메소드를 호출하면 메소드가 내부적으로 예외 결과를 화면에 출력한다
  - return 값이 없기 때문에 print처럼 그냥 사용하면 된다.

### 다양한 예외 처리 방법

여러 에러들에 대해 조건문을 생성하는 방법

```java
try{

}
catch(ArithmeticException e){
  sysout("ArithmeticException")
}
catch(ArrayIndexOutOfBoundsException e){
  sysout("ArrayIndexOutOfBoundsException")
}
catch(Exception e){
  sysout("알수없는 에러")
}
```

> 
- `ArrayIndexOutOfBoundsException` :  인덱스 에러
- `ArithmeticException` : 산술 오류 (0으로 나눈다던지)
- `NullPointerException` : 매개 변수 값이 Null 일 때
- `IllegalArgumentException` : 매개변수가 의도하지 않은 상황 유발 시킬 때
  - 인자로 들어온 값이 적합하지 않을 때
- `IllegalStateException` : 메소드를 호출하기 위한 상태가 아닐 때
  - 현재 동작할 수 있는 상황을 충족시키지 못할 때


catch의 인스턴스로 형식을 정해준다면 저 형태의 에러가 온다면 실행한다.
if else 문처럼 흘러가기 때문에 위의 값들이 실행이 되지 않는다면, 아래로 흐르고 마지막 catch 까지 흘러간다.
마지막의 알수없는 에러가 맨 위에 있다면 상단에서 실행이 되기 때문에 조건 분기가 불가능하다.

### finally

- `finally {L}` L: 예외여부와 관계없이 실행되는 로직

- finally 블록이 사용하는 이유는 clean-up과 연관이 깊다
  - ex ) db를 종료하는 경우

### 예외 던지기

어떤 코드를 실행하는데 이런 에러가 발생한다.

```java
Exception in thread "main" java.lang.Error: Unresolved compilation problems:
    Unhandled exception type FileNotFoundException
```

위 로직에 대한 예외처리가 필요하다는 뜻이다.

기존 코드의 FileReade를 사용할 때, 예외가 발생하는데 그 예외처리를 무조건 해줘야 하는 경우이다.
코드를 수정한다.

```java
try {
    BufferedReader bReader = new BufferedReader(new FileReader("out.txt"));
} catch (FileNotFoundException e) {
    e.printStackTrace();
}
```

### throws

지금까지의 예외처리는`try, catch`를 이용해 처리했다. `try,catch`는 엔드 유저에서 많이 사용된다. 만일 이 코드가 엔드 유저가 아닌 중간 정도에 위치하는 메서드라면, 이 에러를 다음 유저에게 넘길 수가 있다. 이 때 사용하는 방법이 throws이다

```java
void run (){
  try {
    BufferedReader bReader = new BufferedReader(new FileReader("out.txt"));
  } catch (FileNotFoundException e) {
    e.printStackTrace();
  }
}
a.run()
```

원래의 코드이다. 이 코드를 어딘가에서 사용하려고 할때, 그 유저에게 에러처리를 넘기고 싶은 경우의 코드를 수정해보자

```java
void run throws FileNotFoundException (){
  BufferedReader bReader = new BufferedReader(new FileReader("out.txt"));
}
a.run(); => 에러
try{
  a.run()
}
catch(FileNotFoundException e){
  ~
}
```
메서드에 `throws` 를 적고 `try,catch` 를 제거해도된다.
하지만 이젠 `a.run()`에서 에러가 난다. run 메서드를 사용하면서 `FileNotFoundException`에 대한 예외처리가 필수적이기 때문이다.
=> run 메서드에 try catch로 에러처리를 해준다.


### throw = Exception 생성하기
지금까지는 Exception 처리만 했었다
생성하는 법은 간단하다.

```java
public void divide(){
  if (right==0){
    throw new ArithemeticException("0으로 나눌 수 없습니다.")
  }
}
```
throw가 실행되면 메서드가 더 진행되지 않고 끝나게 된다.

### Throwable

어떤 예외는 예외처리를 강제하고 있지만, (`IOException`)
아닌 예외도 있다. (`ArithmeticException`)
그 이유가 무엇일까?

`ArithmeticException` 는 `RuntimeException`의 자식 클래스이고 
`RuntimeException`은 `Exception`의 자식 클래스이다.

`IOException`는 `Exception`의 자식 클래스이다


- Throwable
  - Error 
    - 하드웨어에 문제가 생겼을 때
    - 자바에서 문제가 생겼을 때
    - 우리는 할 수 있는 방법이 없다.
  - Exception
    - IOException
    - RuntimeException
      - ArithmeticException..

---  
> - 부모중에 `RuntimeException`이 있는 예외는 unchecked 예외이다.
- checked 예외 - RuntimeException을 제외한 Exception의 하위 클래스이다

- checked 예외는 반드시 예외처리를 해야 하는 되는 것이고, 
- unchekced는 해도 되고 안 해도 되는 예외다. 


### 나만의 예외 만들기 

#### checked 인지 unchecked 인지 선택하기 
- API 쪽에서 예외를 던졌을 때 API 사용자 쪽에서 예외 상황을 복구 할 수 있다면 checked 예외를 사용한다.
- 하지만 checked 예외를 너무 자주 사용하면 API 사용자를 몹시 힘들게 할 수 있기 때문에 적정선을 찾는 것이 중요하다.

- 사용자가 API의 사용방법을 어겨서 발생하는 문제거나 예외 상황이 이미 발생한 시점에서 그냥 프로그램을 종료하는 것이 덜 위험 할 때 unchecked를 사용한다


나누기 메서드의 오류를 직접 만들어보자 
#### Unchecked(RuntimeException을)
```java
class DivideException extends RuntimeException {
    DivideException(){
        super();
    }
    DivideException(String message){
        super(message);
    }
}
throw new DivideException("0으로 나눌 수 없습니다.");
```
RuntimeException을 상속받아 만들었다. 
생성자를 그대로 받아오고 인자로 들어온 메시지를 돌려준다.

#### checked(Exception)

```java
class DivideException extends Exception {
    DivideException(){
        super();
    }
    DivideException(String message){
        super(message);
    }
}
throw new DivideException("0으로 나눌 수 없습니다."); // => 오류 
```

RuntimeException으로 상속을 받지 않기 때문에 예외를 처리해줘야 한다.

```java
try{
  throw new DivideException("0으로 나눌 수 없습니다."); // => 오류 
}
catch (DivideException e){
  e.printStackTrace();
}
```

