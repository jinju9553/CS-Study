# Interceptor
- Interceptor는 무엇이며 언제 사용할까?
- Interceptor는 어떻게 구현하나?

<br>

## Interceptor

- 컨트롤러가 요청을 처리하기 전/후에 Interceptor를 처리하게 된다.
    - `preHandle` : 컨트롤러가 호출되기 전에 수행한다. 단, false를 반환하게 된다면 리퀘스트가 바로 종료된다.
    - `postHandle` : 컨트롤러 안에서 서비스 호출 등을 마치고 리턴할 때 실행된다.
    - `afterCompletion` : 클라이언트에 응답을 전송한 뒤에 실행된다. 예외가 발생하여도 실행된다.
  
- interceptor는 여러 개를 설정할 수 있으나, 각 interceptor간의 처리 순서에 주의하여 작성해주어야 한다.
- AOP와 유사하나 AOP는 Proxy 기반임에 주의한다. (단순 로직 차원에서의 이전/이후를 구분함)
    - AOP는 웹 관련 기능이 아니기 때문에 interceptor와 다르게 **request와 response에 접근할 수 없다.**

<br>

## interceptor의 적용 예시
  - 만약 웹 서비스에서 로그인 한 사용자만 게시판 이용을 허용할 경우, write와 view, modify와 delete url을 포함하여 로그인 여부 체크를 하는 모든 곳에 interceptor를 적용해준다. (exclude로 제외시킬 url로 지정할 수 있다.)
  
  - 가령, 로그인을 하지 않았다면 서버까지 요청이 넘어가지 않고 interceptor 단에서부터 미리 요청을 차단한다면 처리 시간이 줄어들 것이다.

### 출처
- 개인 필기