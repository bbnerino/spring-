# Overriding
재정의 라고 한다.

> 지금까지의 상속은 부모의 메서드들을 그대로 물려받아서 사용했지만, 그 메서드를 수정해서 새로운 값으로 사용해야 할 수도 있다.


사용법은 간단하다. 부모클래스에서도 선언되고 자식클래스에서도 선언되었다면 그 인스턴스는 자식클래스에서 먼저 메서드를 찾아 실행시키게 된다.

```java
class Calculator {
	public void sum (){
  	 	sysout("옛날 메서드");
	}
}
class newCalculator extends Calculator {
	public void sum (){
    	sysout("고친 메서드");
    }
}
newCalculator c1 = new newCalculator();
c1.sum() => 고친 메서드
```

## 오버라이드의 조건 

부모의 메서드의 형식과 , 자식 메서드의 형식이 같아야 한다.
```java
class Calculator {
	public void sum (){
  	 	sysout("옛날 메서드");
	}
}
class newCalculator extends Calculator {
	public int sum (){
    	return (left+right);
    }
}
newCalculator c1 = new newCalculator();
c1.sum();
```
이 함수는 오류가 날 것이다.
부모 메서드의 형식이 void이고 자식은 int이기 때문에 오버라이드가 되지 않는다.


그 이외에도 몇가지 조건이 있다

> 메소드의 이름
메소드 매개변수의 숫자와 데이터 타입, 순서
메소드의 리턴 타입 (위의 예시)

똑같은 메소드를 가져와서 사용하는 방법
```java
class Calculator {
	public int sum (){
    	return (left+right);
	}
}
class newCalculator extends Calculator {
	public int sum (){
    	return super.sum()
    }
}
newCalculator c1 = new newCalculator();
c1.sum();
```
하위 클래스에서는 super를 사용하여 상위 클래스의 메서드의 return 값을 그대로 사용할 수 있고,부가적인 동작이 더 필요하다면 추가하면 된다.


# OverLoading

같은 이름의 메서드이지만 서로 다른 매개변수를 갖는 경우를 뜻한다.
=> sum(1,2) 도 가능하고 sum(1,2,3)도 가능하다?

> 자바에서는 같은 이름의 메서드라도 다른 매개변수가 들어가는 메서드라면 서로 다른 메서드라고 인식한다.


```java

class  Calculator {
	public void sum (int left,int right){
    	sysout (left+right);
	}
	public void sum (int left,int right,int third){
    	sysout (left+right+third);
    }
}
Calculator c1 = new Calculator();
c1.sum(1,2);
c1.sum(1,2,3);

```

 다른 방법으로 사용해보자 
 ```java
class  Calculator {
	int left, right;
    int third = 0;
	public void setOprands (int left,int right){
    	this.left = left;
        this.right = right;
	}
	public void setOprands (int left,int right,int third){
    	this.left = left;
        this.right = right;
        this.third = third;
    }
    public int sum (){
		return (left+right+third)    
    }
}

```


여기서는 지역변수에 할당을 하는데 setOprands 안에서 left,right의 코드가 겹친다.
이럴 경우에는 중복을 피하기 위해 아래와 같이 사용하는 것이 좋다.
```java
	public void setOprands (int left,int right,int third){
    	this.setOprands(left,right);
        this.third = third;
    }
```
같은 이름의 메서드를 사용하였지만 역시나 매개변수의 개수가 다르기 때문에 다른 것으로 인식한다.

> # 오버라이딩 vs 오버로딩
오버라이딩은 같은 매개변수, 같은 이름일 때, 메서드의 내용을 재 정의
오버로딩은 같은 이름 다른 매개변수일 경우 동일한 메소드 이름으로 여러개 정리 


