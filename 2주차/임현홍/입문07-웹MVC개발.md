# 회원 관리 예제 - 웹 MVC 개발

지금까지 만들었던 로직들을 이용해서 MVC 로 만들어보자 


### 홈 화면 
`localhost:8080/` 으로 접근했을 때 아래와 같은 페이지가 나오게 한다

![](https://velog.velcdn.com/images/hey-hey/post/f955b08e-653b-4d40-9b93-1e0efdf7461a/image.png)

#### Controller 생성
HomeController 를 생성해 get('/') 요청이 들어왔을 때, 정적인 페이지 home.html를 반환한다.
```java
package hello.springgood.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {
    @GetMapping("/")
    public String Home(){
        return "home";
    }
}
```

#### View 생성
```html
<body>
  <h1>MY SWEET HOME</h1>
  <div>
    <a href="/members/new">회원가입</a>
    <a href="/members">회원 목록</a>
  </div>

</body>
```
회원 가입 버튼을 누르면 `/members/new` 페이지로 이동되고
회원 목록 버튼을 누르면 `/members` 페이지로 이동된다.

#### Controller 생성 
members 와 관련된 컨트롤러를 생성한다. => `MemberController`

컨트롤러에서는 서비스를 이용해 데이터에 접근을 해야한다.
MemberService를 만들어주고, memberController는 memberService 생성자 주입으로 등록을 해주고 사용하면 된다.

```java
@Controller
public class MemberController {
    private final MemberService memberService;

    @Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }
}
```
### 회원가입 화면
`localhost:8080/members/new` 화면

![](https://velog.velcdn.com/images/hey-hey/post/99e1df6d-f6a5-4c52-9e95-ef7536d4c381/image.png)
#### Controller 추가
위에서 만들어준 Controller에 추가한다.
```java
@GetMapping("/members/new")
public String createForm(){
    return "members/createMemberForm";
}
``` 

#### View 생성
`members/createMemberForm.html` 파일을 만들어 준다.
```java
<form action="/members/new" method="post">
  <label for="name">이름</label>
  <input type="text" id="name" name="name" placeholder="이름을 입력하세요">
  <button type="submit">등록</button>
</form>
```
- form 안의 action을 통해 api를 작성하고 method를 입력해준다.
- input의 name을 통해 body의 데이터를 확인할 수 있다. 

#### form 생성
`{name : "Hey-hey"}` 의 값을 정해주는 form 이 필요하다.
`controller/MemberForm`
```java
public class MemberForm {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

post('/members/new') 요청을 컨트롤러에 추가한다.

#### Controller 추가
```java
@PostMapping("/members/new")
public String create(MemberForm memberForm){
    Member member = new Member();
    member.setName(memberForm.getName());

    memberService.join(member);
    return "redirect:/";
}
```
memberForm으로 받아온 값을 member 인스턴스로 만든다.
memberService의 join을 통해 repository에 추가해준다.
페이지를 home('/')으로 이동 시켜준다.


### 회원 목록 화면
`localhost:8080/members` 화면

![](https://velog.velcdn.com/images/hey-hey/post/0d53aab3-fe15-43f2-8010-f4e69ee77c47/image.png)

#### Controller 추가
Controller에 회원목록 화면을 추가한다.
```java
@GetMapping("/members")
public String list(Model model){
    List<Member> members = memberService.findMembers();
    model.addAttribute("members",members);
    return "members/memberList";
}
```

이번에는 전체 member 목록을 불러와 템플릿엔진에서 사용이 가능하게끔 전달해주었다.

#### View 추가
```html
<html xmlns:th="http://www.thymeleaf.org">
<tr th:each="member :${members}">
  <td th:text="${member.id}"></td>
  <td th:text="${member.name}"></td>
</tr>
```
템플릿 엔진을 import 해주고 하나씩 보여준다. 
자세히는 모르지만 템플릿 엔진 문법인가 보다.

간단하게 MVC 작업을 완료했다. 하지만 서버를 껐다 켜면 리포지토리가 초기화되는 중이다.
이것을 이제 DB에 저장하는 방법을 배워야겠다. 