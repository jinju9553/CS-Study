# MVC 프레임워크
- MVC 프레임워크의 구성 요소는?
- MVC 구조는 어떻게 동작할까? 
<br></br>


## 구성 요소
---
### 📌 Dispatcher Servlet
- 모든 request를 처리하는 **중심 컨트롤러** 격 존재. Controller의 프론트 부분이라 볼 수 있으며, 모든 클라이언트의 요청을 처리한다.

- 서블릿 컨테이너에서 **HTTP 프로토콜을 통해 들어오는 모든 request**를 프로그램의 제일 앞단에서 **중앙 집중식으로 처리**해준다.

- Servlet Class이며, 컨트롤러에게 클라이언트의 요청을 전달하고, 컨트롤러가 리턴한 결과값을 View에 전달하여 알맞은 응답을 생성한다.

- `Handler Adapter` : Dispatcher Servlet의 처리 요청을 변환해서 컨트롤러에 전달하고, 컨트롤러의 응답 결과를 Dispatcher Servlet이 요구하는 형식으로 변환한다.
<br></br>


### 📌 Handler Mapping
- 클라이언트의 request URL을 **어떤 컨트롤러가 처리해야 할 지를 찾고**, Dispather Servlet에게 **전달**해준다.

- 즉, URL 과 컨트롤러의 **Mapping**을 관리한다. 컨트롤러 상에서 `@RequestMapping` 어노테이션으로 매핑된 URL을 이 핸들러가 찾아준다.
<br></br>


### 📌 Controller
- 클라이언트의 실질적인 요청을 처리하는 부분. Dispatcher Servlet을 프론트 컨트롤러라고 본다면, 이곳은 백엔드 부분의 컨트롤러라고 볼 수 있다.

- 모델의 **처리 결과를 담아 Dispatcher Servlet에게 반환**한다.
    - 처리 결과는 `Model` 또는 `ModelAndView`에 저장된다.
<br></br>


### 📌 View Resolver
- View를 찾는 객체이다. 컨트롤러의 처리 결과를 나타낼 View를 결정하는 역할을 담당한다.

- 컨트롤러(Action)의 처리 결과를 생성할 **View를 결정**하고, 컨트롤러가 리턴한 View 이름으로 실행될 **JSP 경로를 완성**시킨다.
<br></br>


## 동작 과정
---
1. 클라이언트가 URL을 요청하면, 웹 브라우저에서 스프링으로 request가 전송된다.

2. `Dispatcher Servlet`이 request를 수신하면 `Handler Mapping`을 통해 해당 URL을 담당하는 `Controller`를 찾아낸다.

3. 찾아낸 `Controller`로 request를 전송하고, 여기에 필요한 `Model`을 구성한다.

4. `Model`에서는 페이지 처리에 필요한 정보를 가져온다. (DB에 접근하여 쿼리문을 통해 값을 반환받는다.)

5. DB를 통해 얻은 `Model` 정보를 `Controller`에게 응답(response)으로 전송한다. 
    - 이를 수신한 `Controller`는 `Model`을 완성시키고 `Dispatcher Servlet`에게 전달한다.

6. `Dispatcher Servlet`이 `View Resolver`를 통해 request에 해당하는 View 파일을 찾아온다.

7. 받아온 View 페이지에 `Model`을 전송한 후, 클라이언트에 보낼 페이지를 완성시킨다.

8. 완성된 View 파일을 클라이언트에게 response로 전송하고 화면에 출력한다.
<br></br>


### 출처
- 최범균, \<웹 개발자를 위한 Spring 4.0 프로그래밍\>, 가메 출판사 (2018)
- https://velog.io/@miscaminos/Spring-MVC-framework
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/Spring/Spring%20MVC.md