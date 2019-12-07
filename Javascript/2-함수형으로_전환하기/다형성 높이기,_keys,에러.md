### 다형성 높이기, _keys, 에러

### _each에 null 넣어도 에러 안나게 하기

AS-IS : each 에 null을 넣으면 에러 발생
TO-BE : each 내부 함수에 length 를 참조하는 부분을 get 함수로 대체하여 null을 넣어도 undefined 가 되어 에러없이 함수가 끝남

함수형 프로그래밍은 형 체크, try catch 를 사용하지 않더라도 예외 데이터가 들어왔을 때, 에러가 나지 않고 정확하게 프로그래밍 할 수 있다.

```javascript
_each(null, console.log)
_map(null, v => v);

let _length = _get('length');

function _each (list, iter) {
  for (let i = 0, len = _length(list); i < len; i++) {
    iter(list[i]);
  }
  return list;
}

```


### _keys 만들기
### _keys에서도 _is_object 인지 검사하여 null 에러 안나게 하기

```javascript
console.log(Object.keys({ name: 'ID', age: 33 }));
console.log(Object.keys(null)); // error

function _is_object (obj) {
  return typeof obj === 'object' && !!obj;
}

function _keys(obj) {
  return _is_object(obj) ? Object.keys(obj) : [];
}
```

### _.each 외부 다형성 높이기

each 에 인자값으로 Array, Object 둘 다 들어와도 정상 작동하게끔 다형성을 높인다.

```javascript
function _each(list, iter) {
  let keys = _keys(list);
  for (let i = 0, len = keys.length; i < len; i++) {
    iter(list[keys[i]]);
  }
  return list;
}

_each({
  13: 'ID',
  19: 'HD',
  29: 'HD'
}, name => {
  console.log(name);
})
_go(
  {
    13: 'ID',
    19: 'HD',
    29: 'HD'
  },
  _map(name => name.toLowerCase()),
  console.log
)
```