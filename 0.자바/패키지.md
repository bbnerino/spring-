# 클래스패스 
컴퓨터의 저장장치 어딘가에 존재하는 클래스 파일을 사용하기 위한 방법

다음과 같은 파일이 있다.

ClasspathDemo.java
```java
class Item{
}
class ClasspathDemo{
}
```
컴파일을 하게 되면 `javac ClasspathDemo.java`

- ClasspathDemo.class
- Item.class
즉 클래스 하나는 하나의 클래스 파일이 된다는 것을 알 수 있다.

## 파일 찾기
`java -classpath ".;lib" ClasspathDemo`

- classpath : 자바를 실행할 때 사용할 클래스들의 위치를 가상머신에게 알려주는 역할이다.

### .;lib

- `.` 현재 디렉터리에서 클래스를 찾는 의미이다
- `;` 경로와 경로를 구분해주는 구분자
- `lib` 현재 디렉터리에 없다면 현재 디렉터리의 하위 디렉터리 중 lib에서 클래스를 찾겠다는 의미

# 패키지
여러개의 클래스가 존재할 때, 하나의 클래스 안에서 같은 이름의 클래스들을 사용하기 위한 방법

java 파일의 location를 살펴보면
`/src/org/opentuto/javatuto/object/CalculatorDemo.java` 일때,
이 파일의 상단에는
`package org.opentuto.javatuto.object`이라는 구문이 있다.

> 패키지는 기본적으로 디렉터리와 일치한다. 그렇기 때문에 아래의 패키지들은 물리적으로 같은 디렉터리에 존재할 수 없다.
- org.opentutorials.javatutorials.object
- org.opentutorials.javatutorials.classninstance 

다른 패키지에 있는 클래스를 사용하고 싶을 때
```java
package org.opentutorials.javatutorials.packages.example2;
import org.opentutorials.javatutorials.packages.example1.A;
 
public class B {
    public static void main(String[] args) {
        A a = new A();
    }
}
```

`import org.tutotutorials.javatutorials.packages.example1.A`
A 대신에 `*`을 쓰면 와일드 카드로 모든 내용을 불러올 수 있다.

## API 와 API 문서 보는 것
`System.out.println(1);`
System이라는 클래스는 어디서 불러올까?
`import java.lang.*;`를 통해 불러오지만
java는 자동으로 이 값을 불러와준다.

 패키지 `java.lang.*`의 클래스들도 자바에서 제공하는 API 중의 하나라고 할 수 있다.
