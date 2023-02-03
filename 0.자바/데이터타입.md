# 설치

https://www.oracle.com/kr/java/technologies/downloads/#jdk19-windows

jdk 설치

JRE 설치

![](https://velog.velcdn.com/images/hey-hey/post/95a4438f-be56-4fa8-afb5-e298b2856b3a/image.png)


vscode 에서 실행
java extenstion 설치 후
view - 명령팔레트 - java:create Java Project - No Build Tools - 프로젝트 명 입력 
```java
public class App {
    public static void main(String[] args) throws Exception {
        System.out.println("Hello, World!");
    }
}

```
실행 시키면 Hello World 출력 완료 

src 밑의 하나하나가 패키지 이다


# 숫자 

- 정수 : 소수점 없는 숫자 (int)
- 실수 : 소수점 붙는 숫자 (double)


# 문자 
- 문자 : 문자는 한글자를 의미하고 
- 문자열 : 여러개의 문자가 결한한 것을 의미

문자 : ' 작은 따옴표 안에 적어야한다.
문자열 : " 큰 따옴표 안에 적어야 한다.

![](https://velog.velcdn.com/images/hey-hey/post/1b84c9ad-eed6-4346-b3c5-fa4411c94476/image.png)

역슬래쉬 `\"` 를 사용하면 문자열 안에서 사용가능하다
`\n` or `원화(w)n` 를 사용해 다음줄로 이동한다.

# 변수 

데이터를 담는 컨테이너 이며, 데이터의 형식이 맞지 않으면 실행도 되지 않는다.

```java
int a ;
a = 1
sysout(a) => 1
```
`int a` 
int = 데이터 형식 
a = 변수의 이름
`a=1`
a=1 대입하기

> 정수 (int) 자리에 실수를 넣는다면?
int a ;
a= 3.5 ; => 에러 발생


# 데이터 타입 

### 정수형 
- int : 대부분의 경우 사용
- byte : -128~127
- short : -32768 ~ 32767
- long : 엄청작은숫자 ~ 엄청큰숫자

=> 선택하는 숫자 타입에 따라 사용하는 메모리가 다르다.

ex) long a = 1 이라도 8바이트를 사용하게 된다.

```JAVA
long a ;
a = 123123123123 
```
일 때 에러가 난다. 왜 ? 123123123123 이 int의 범위를 넘어섰기 때문에 int라고 판단했었는데 long의 자리에 들어갔기 때문이다.
=> `a= 123123123123L` 의 방법으로 이 숫자가 long이라는 것을 명시해준다.

### 실수형 
- float : 소수점 7자리까지 표현
- double : 소수점 16가지까지 표현
정밀도의 차이인데, 웬만하면 double로 사용하면 된다.
float를 사용할때는 1.0f 이런 식으로 사용해야한다. 
=> F 는 Float 데이터 타입이라는 것을 명시 


### 문자
- char : 모든 유니코드 문자

# 형변환


### 암시적 형 변환(자동)
`double a = 3.0F`
java가 자동으로 F를 double로 변환해준다.

`float a = 3.0` 
3.0은 double이다 하지만 double > float 이므로 double이 float가 되면 데이터를 손실할 수도 있기 때문에 자동으로 변환해주지 않는다.

> 형변환 크기 확인
byte => short/char => int => long => float => double

### 명시적 형 변환(수동)

`float a = 100.0`
100.0은 double이라서 에러가 난다.
위에서처럼 100.0f 라고 사용해도 되지만 명시적으로 하는 방법이 있다.
`float a = (float) 100.0 `
