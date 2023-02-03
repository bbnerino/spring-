연산자에는 크게 아래와 같이 있다.
- 대입 연산자
- 산술 연산자
- 비교 연산자 
- 논리 연산자 

# 산술 연산자
산술할 때 사용되는 연산자
더하기 빼기 ... 
+ - * / %(나머지) 

# 비교연산자 


Boolean = 참과 거짓 
`==` 좌항과 우항을 비교해서 서로 값이 같다면 true 다르면 false 
`!=` , `<` , `>` 다 알죠?

`.equals` = 문자열을 비교할 때 사용하는 메소드 

# 조건문
```java
if( true / false) {
	then 절
}
else if(true/false){
	blabla~~
}
else{
	~~
}
```

# 논리 연산자 

조건문을 보좌하는 역할 
- `&&` (and)
- `||` (or)
- `!` (not)

# 반복문
### while

```java
while(조건){
	반복 내용
}
```
예시)

```java
int i = 0;
while(i<10){
	sysout(i);
    i++;
}
```

### for 

```java
for(초기화;종료조건; 반복실행){
	반복 내용
}
```
예시)
```java
for(int i=0; i<10 ; i++){
	sysout(i);
}
```

### break
```java
int i = 0;
while (true) {
	i++;
	System.out.println(i);
	if (i == 10)
		break;
}
```

### continue 
실행을 즉시 중단하면서 반복은 지속하고 싶을 때 사용

```java
int i = 0;
while(true){
	i++;
    System.out.println(i);
    if (i==5)
    	continue;
}
```
=> 결과 => 1,2,3,4,6,7,8,9,10...


# 배열 
연관된 데이터를 모아서 관리하기 위한 데이터 타입

```java
String[] newList = {"hi","bye"}
```
잉? 왜 대괄호가 아닌거지... 

## for - each
```java
String[] members = {"hi","hi2","hi3"}
for (String e : members){
	sysout(e)
}
```
- `e` :`members` 
- 콜론 뒤의 `members` 의 항목 하나하나 `e`


## 배열에서의 오류 
### IndexOutOfBoundsException
존재하지 않는 인덱스를 사용하려고 했을 때 발생 

```java
String[] members = new String[3];
members[3] = "들어가나" ; => 오류 

```
### 컬렉션
컬렉션이라는 기능으로 (== Container라고도 불린다.) 유연하게 배열을 사용할 수 있다. 
