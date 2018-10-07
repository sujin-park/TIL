# 입력양식 - form

`<input>` 태그란 사용자로부터 데이터를 입력받을 수 있는 필드를 만들어준다.

- type : 어떤 타입의 필드를 만들지 정한다.
  - text : 텍스트 입력
  - password : 패스워드 입력 (텍스트 가려짐)

- submit : 입력한 데이터를 제출
- name : 서로 다른 값들을 구분하기 위해 이름을 지정하여 값들을 매핑

`<form>` 태그는 사용자로부터 데이터를 받아 서버에 제출 할 수 있게 해준다.
- action : 입력받은 데이터를 어느 url에 제출할 것인지 정한다.

```html
<html>
  <body>
    <form action="http://localhost/login">
      <p>아이디 : <input type="text"></p>
      <p>비밀번호 : <input type="password"></p>
      <input type="text">
      <input type="submit">
    </form>
  </body>
</html>
```
