> 프로그램이 커지면 여러 가지 이유로 이름이 충돌하게 된다. 이를 해결하기 위해 고안된 것이 유효범위라는 개념이다. 


### 전역변수 
클래스 변수 라고도 부를 수 있다.


### 지역변수 
메소드 안에서 선언된 변수 

```java
public class ScopeDemo {
    
    static void a() {
        int i = 0;
    }
 
    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {
            a();
            System.out.println(i);
        }
    }
 
}
```
1. i 가 전역변수로 선언이 된다.
전역변수로 선언된 변수는 모든 메서드에서 사용이 가능하다.
2. i 가 a 메소드 안에서 선언이 된다.
메소드 안에서 선언된 변수는 그 메소드 안에서만 사용이 가능하다.
전역변수 i와 이름이 같지만 메서드 안에서 선언된 i의 값이 그 메서드에서 사용되게 된다. 

3. for문안에서 i 가 선언 (int i) 이 된다.
for 문도 하나의 메서드이기 때문에, 전역변수 i의 값과는 영향이 없다.


## 정적인 유효범위
lexial scope == static scope

## 동적인 유효범위 
dynamic scope 

> 메소드 a,b가 존재하는데 a에서 선언한 i 가 10일 때 메소드 b에서 사용한 i도 10아라면 메소드 b는 a의 유효범위에 소속된 것이라고 할 수 있다. 
근데 그럴리가 없다. 대부분의 현대적인 언어들이 정적 스코프 방식을 선택하고 있고 자바도 마찬가지이다.

# 인스턴스의 유효범위
지금까지의 내용은 클래스 내에서의 유효범위를 알아보았다.
인스턴스에서도 동일하지만 `this`의 사용에서 차이점이 생기게 된다.

```java
class C {
	int v= 10;
    void m(){
    	int v = 30;?
        sysout(v) ; 메소드 안에서 사용된 지역변수 v
        sysout(this.v) ; 
    }
}
C c1 = new C();
c1.m()
```
인스턴스 자신을 의미하는 `this`를 사용하게 되면 전역변수 v에 접근 가능하다.

# 초기화 / 생성자
지금까지 Calculator라는 클래스를 사용할 때,우리는 setOprands라는 메소드에 l,r 값을 넣어서 값을 넣어 줘야,다른 메소드를 사용할 수 있었다. 

```java
Calculator c1 = new Calculator();
c1.setOprands(10,20);
c1.sum();
```
이 과정을 `new Calculator(10,20)` 이런식으로 초기화할 수 있다면 편할 것같다.

### 사용법
```java
class Calculator{
	int left,right;
	public Calculator(int left,int right){
    	this.left = left;
        this.right = right
    }
}
```

클래스 내에서 생성자를 만드는 법은 **같은 클래스 이름**으로 메서드를 선언해주면 된다.

js 에서 constructor 와 사용법이 유사하다.
