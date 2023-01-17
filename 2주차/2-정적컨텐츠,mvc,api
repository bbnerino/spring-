# 정적 컨텐츠, MVC, API
1. 정적 컨텐츠 
- 파일을 그대로 웹으로 보내 주는 것
2. MVC / 템플릿 엔진
- html을 프로그래밍 해서 동적으로 바꿔서 보내 주는 것
3. API 
- JSON 데이터 포맷으로 보내서 사용하는 것

## 정적 컨텐츠 
원하는 파일을 src/main/resources/static/00.html 로 생성한다.
localhost:/00.html 로 접근하면 이 파일을 열어볼 수 있다.

#### 원리 
- localhost:/00.html 접근 
- 톰캣 서버에서 받고 스프링으로 넘긴다.
- 00 컨트롤러를 찾아본다 
- 그 컨트롤러가 없다면 static에서 00.html 파일을 찾아서 보내준다.

## MVC 
- Model
- View
- Controller

예전 방식 : View + Model이 함께 묶인 형태 (앞선 글에서의 예제)

- View 는 관심사를 분리해야 한다.
  - 화면을 그리는 것만 해야한다.
  - 비지니스 로직과 내부적인 것은 Controller에서 해야 한다. 


### 템플릿 엔진 2
이번에는 params를 이용해서 값을 받아오는 로직이다.

```java
@Controller
public class HelloController {

    @GetMapping("hello-mvc")
    public String helloMvc(@RequestParam("name") String name,Model model){

        model.addAttribute("name",name);
        return "hello-mvc";
    }
}
```
`@RequestParam("name") String name,Model model`
Params로 name="" 의 값을 불러와서 그 값을 template에서 보여준다. 
http://localhost:8080/hello-mvc?name=바보멍충이
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
  <h1 th:text="${name}">이름</h1>
</body>
</html>
```


# API

api 를 만드는 것의 초기단계부터 알아보자
```java
@GetMapping("hello-string")
@ResponseBody
public String helloString(@RequestParam("name") String name,Model model){
    model.addAttribute("name",name);
    return "hello-mvc";
}
```

`ResponseBody` = http 에서 body 부에 이 응답을 주겠다.
=> View 로 가는 것이 아니라 이 문자 그대로가 return 된다.

/hello-api?name=바보멍충이 
=> `바보멍충이` 출력

### JSON 형식으로 넘겨줘보자 

JSON으로 넘겨주기 위해 Object를 생성해주는 Class를 하나 만든다.
```java
static class Hello{
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```
이 클래스를 이용해 return 으로 Hello라는 Class를 응답으로 보내준다.
```java
@GetMapping("hello-api")
@ResponseBody
public Hello helloApi(@RequestParam("name")String name,Model model){
    Hello hello = new Hello();
    hello.setName(name);
    return hello;
}
```

/hello-api?name=바보멍충이 
=> `{"name": "바보멍충이"}` 출력

***getter,setter***
프로퍼티 방법 , 게터세터 
`ctrl + enter` 단축키로 선택 

#### 작동방식
`@ResponseBody` 를 이용해서 Hello라는 객체가 들어오면
`viewResolver` 대신에 `HttpMessageConverter`에서 
JSON일 때 JSONConverter (기본 객체 처리) - Jackson2
문자일 때는 StringConverter (기본 문자처리) 
가 동작해서 응답을 해주게 된다. 
