# OOP 
Object Oriented Programing
객체 지향 프로그래밍은 좀 더 나은 프로그램을 만들기 위한 프로그래밍 패러다임으로 로직을 **상태** (state)와 **행위 **(behave)로 이루어진 객체로 만드는 것이다.

> 쉽게 얘기해서 변수와 메소드를 그룹핑한 것.

## class 
  - instance를 만들기 위한 설계도 
  - 정의
  
## instance 
  - class로 만든 구체적인 제품
  - 객체
  - 호출


중복을 제거하고 재사용성을 높이는 방향을 위한 설계 

---
```java
class Calculator{
	int left,right;
    
	public void setOprands(int num1,int num2){
    	this.left = num1;
        this.right = num2;
    }
    public void sum (){
    	sysout(this.left+this.right);
    }
    public void avg (){
    	sysout((this.left+this.right)/2);
    }
}
```
```java
Calculator c1 = new Calculator();
c1.setOprands(10,20);
c1.sum();
c1.avg()

Calculator c2 = new Calculator();
c2.setOprands(30,40);
c2.sum();
c2.avg()
```
- Calculator = 클래스
- c1, c2 = 각각의 인스턴스 
  - 각각의 상태가 다르다

## 클래스 맴버 
클래스의 구성원 ?
클래스 변수 
클래스 메소드

### 클래스 변수 
```java
class Calculator {
	static double PI = 3.14;
    int left,right ;
    ...
}
```
`static`을 붙이면 클래스의 변수가 된다.

```java
Calculator c1 = new Calculator();
sysout(c1.PI); => 3.14
sysout(Calculator.PI); => 3.14

```
인스턴스를 생성하지 않아도 클래스 변수에 접근하면 사용 가능하다.

```java
class Calculator {
	static double PI = 3.14;
    int left,right ;
    public void usePI(){
    	sysout(this.left+this.right + PI)
    }
}
```

클래스 내에서 사용할 때 this를 붙이지 않고 PI를 사용할 수 있다.
왜 ? this를 붙이는 이유는 instance 마다 다른 값을 들고 있기 때문이지만, class 변수는 this없이 사용하다.

> 클래스 변수의 용도
- 인스턴스에 따라서 변하지 않는 값이 필요할 경우 (final로 선언하면 불변)
- 인스턴스를 생성할 필요가 없는 값을 클래스에 저장하고 싶을 경우
- 값의 변경 사항을 모든 인스턴스가 공유해야할 경우 


### 클래스 메소드
```java
class Calculator {
	public static void sum(int left,int right){
    	sysout(left+right);
    }
}
Calculator.sum(10,20); => 30
```			
static을 사용한 함수는 클래스에 직접 접근해 부를 수 있다.
(굳이 인스턴스가 left,right 값을 가지고 있을 필요가 없다)



>1. 인스턴스 메소드는 클래스 맴버에 접근할 수 잇다.
2. 클래스 매소드는 인스턴스 맴버에 접근할 수 없다.


