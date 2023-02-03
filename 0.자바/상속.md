## Inheritance 
상속은 객체지향에서 가장 중요한 개념이다. 
상속은 객체지향의 재활용성을 극대화시킨 프로그래밍 기법

> 상속 : 어떤 객체가 있을 때 그 객체의 필드(변수)와 메소드를 다른 객체가 물려 받을 수 있는 기능. 기존의 객체를 그대로 유지하면서 어떤 기능을 추가하는 방법 

- 부모 클래스 = super class = base class
- 자식 클래스 = sub class = derived class

```java
class Calculator {
	int left,right;
    public void setOprands(int left,int right){
    	this.left = left;
        this.right = right;
    }
	public void sum(){
    	sysout(this.left + this.right) 
    }
    public void avg(){
    	sysout((this.left + this.right)/2) 
    }
}
```

이 클래스에 빼기 메서드를 추가하고 싶다 

```java
class SubCalculator extends Calculator{
	public void substract(){
    	sysout(this.left-this.right)
    }
} 
SubCalculator c1 = new SubCalculator();
c1.setOprands(10,20);
c1.subsctract(); => -10
```

## extends
extends 를 이용해서 class를 선언하면 부모 클래스인 Calculator의 변수들을 사용 가능하다.

물론 상속받아 만든 클래스는 또 다른 곳에서 상속 또한 가능하다.


### 응용하기
Calculator 클래스는 setOprands(a,b)를 해주어야 값이 들어가서 사용이 가능했다. 
만일 Calculator 의 생성자가 있을때 (Calculator(10,20)) 이러한 생성자 메서드를 자식에서도 똑같이 사용하는 방법은 어떻게 될까 

```java
class Calculator{
	public void Calculator(int left,int right){
    	this.left = left;
        this.right = right;
    }
}
class SubCalculator extends Calculator{
	public void SubCalculator(int left,int right){
    	this.left = left;
        this.right = right;
    }
}
SubCalculator c1 = new SubCalculator(10,20)

```
원래의 형태라면 이런식으로 사용하면 에러가 난다 => 왜?
Calculator를 선언할 때 생성자를 넣어줘야하는데, 없기때문이다.
1차적으로 이것을 수정하는 방법은 다음과 같다.
```java
class Calculator{
	public void Calculator(){}
	public void Calculator(int left,int right){
    	this.left = left;
        this.right = right;
    }
}
```
`public void Calculator(){}` 를 추가해줬더니 에러가 나지 않는다
-> 생성자로 아무 값도 안줘도 진행이 된다

하지만 우리가 원하는 것은 부모 클래스를 건드는 것이 아니라 상속받는 클래스를 바꾸고 싶다. 


# super

```java
class SubCalculator extends Calculator{
	public void SubCalculator(int left,int right){
    	super(left,right);
    }
}
```


`super` 키워드는 부모 클래스를 의미한다. 
즉 SubCalculator(a,b)으로 사용하면 그 생성자는 부모 클래스의 생성자로 사용될 수 있다

> super의 주의사항이 있다. 하위 클래스의 생성자에서 가장 먼저 적혀야 한다. 부모 클래스가 먼저 초기화 되고, 자식이 변해야 하는 구조이기 때문이다.
