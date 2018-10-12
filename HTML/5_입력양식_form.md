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

# 입력양식 - 선택

`<option></option>` 태그는 선택할 수 있도록 select 태그로 묶어주어야 한다.
묶어주면 dropdown or combobox 라고 하는 셀렉트 박스로 변경된다.

* option 선택했을 때 값 이름을 color 라고 설정
* 컴퓨터에게 전송할 때는 option value 속성을 통해서 값을 정의
* select 태그에 multiple 이라는 속성 이름만 주면 다중 선택이 가능하다.

```html
<select name="color" multiple>
  <option value="red">붉은색</option>
  <option value="black">검은색</option>
  <option value="blue">파란색</option>
</select>
```
