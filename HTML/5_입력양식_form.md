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

## 체크박스, 라디오

### 라디오버튼

`type = radio, name`이 다른 경우에는 체크해도 둘 다 체크가 되어있는 상태로 남아있지만,
name값이 같은 것들끼리 그룹화가 되고 그룹화된 버튼 중 하나가 체크되면 다른버튼은 해제된다.

```html
<input type="radio" name="color" value="red">
<input type="radio" name="color" value="black" checked>
<input type="radio" name="color" value="blue>
```

### 체크박스

같은 name을 가지고 있는 체크박스들을 다중으로 선택할 수 있다.
checked 속성을 미리 주면 페이지가 reloding 되어도 기본으로 선택이 되어있다.

```html
95 : <input type="checkbox" name="color" value="red">
100 : <input type="checkbox" name="color" value="black" checked>
105 : <input type="checkbox" name="color" value="blue>
```
