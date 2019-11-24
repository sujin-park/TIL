# 파이프라인, _go, _pipe 만들기

### 파이프라인 만들기
- pipe 함수는 여러개의 함수를 인자값으로 받아서 함수를 return 해준다.
```javascript
function _pipe () {
  let fns = arguments;
  return function (arg) {
    return _reduce(fns, function (arg, fn) {
      return fn(arg);
    }, arg);
  };
}

let f1 = _pipe(
  function (a) { return a + 1 }, // 2
  function (a) { return a * 2 }, // 4
  function (a) { return a * a } // 16
);

console.log( f1(1) );
```
### _go 만들기
- pipe 와 비슷하지만 첫 번째 인자로 값, 두 번째부터는 함수를 인자로 받아서 즉시 실행시키고 결과값을 반환해주는 함수이다.

```javascript

function _go (arg) {
  let fns = _rest(arguments);
  return _pipe.apply(null, fns)(arg);
}

_go(1,
  function (a) { return a + 1 }, // 2
  function (a) { return a * 2 }, // 4
  function (a) { return a * a }, // 16
  console.log // 16 출력
);
```

### users에 _go 함수 적용하기

1. _go 함수 적용하기 전
```javascript
console.log(
  _filter(users, function(user) { return user.age >= 30; }))

console.log(
  _filter(users, function(user) { return user.age < 30;}))
```

2. _go 함수 적용 후
```javascript
_go(users,
  function (users) {
    return _filter(users, function(user) {
      return user.age >= 30;
    })
  },
  function (users) {
    return _map(users, _get('name'));
  },
  console.log
)

_go(users,
  function (users) {
    return _filter(users, function(user) {
      return user.age > 30;
    })
  },
  function (users) {
    return _map(users, _get('age'));
  },
  console.log
)
```

3. _curryr 적용
```javascript

let _map = _curryr(_map),
    _filter = _curryr(_filter);
  
_go(users,
  _filter(users, function(user) { return user.age >= 30; }),
  _map(users, _get('name')),
  console.log
)

_go(users,
  _filter(user => user.age > 30),
  _map(_get('age')),
  console.log
)
```

### 화살표 함수 간단하게

```javascript
let a = function (user) { return user.age >= 30; };
let a = user => user.age >= 30;

let b = function (a, b) { return a + b; };
let b = (a, b) => a + b;

let c = (a, b) => ({ val: b }); // 객체 return
```