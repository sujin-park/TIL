# 커링

1. _curry, _curryr
- 인자로 본체함수를 받고, curry 함수를 실행하면 즉시 함수를 리턴하게 된다. 그리고 리턴하는 함수는 또한 인자를 받는다. 미리 받았던 함수를 안쪽에서 검증해준다. 필요한 인자를 채울때까지 함수 본체를 실행하지 않게 만든다.
```javascript

function _curry(fn) {
  return function(a) {
    return function(b) {
      return fn(a, b);
    }
  }
}

/**
* add maker 만들기
*/ 
var add = _curry(function(a, b) {
  return a + b;
})

/**
* 위의 curry 함수는 이런식으로 사용하거나
*/ 
var add10 = add(10);
console.log( add10(5) ); // 15
/**
* 이런식으로 사용한다.
*/
console.log( add(5)(3) ); // 8

```

만약에 아래의 코드처럼 한번에 인자 여러개를 보내서 실행하고 싶다면, 아래와 같은 코드로 변경하면 가능하다.
아래와 같이 변경하면 위의 상황도 사용 가능하고 아래도 정상 작동한다.
```javascript

function _curry(fn) {
  return function(a, b) {
    return arguments.length === 2 ?fn(a, b) : function(b) { return fn(a, b); }
  }
}

var add = _curry(function(a, b) {
  return a + b;
})


console.log( add(1, 2) );
```

### curry 함수로 빼기 함수 만들기
```javascript

var sub = _curry(function(a, b) {
  return a - b;
})

console.log( sub(10, 5) ) // 5

var sub10 = sub(10);
console.log( sub10(5) ); // 결과 -5
```

### curry 함수의 인자를 오른쪽에서 왼쪽으로 사용하기 (curry right)
- 동일한 동작이지만 오른쪽의 인자부터 적용해 나가는 함수

```javascript
function _curryr(fn) {
  return function(a, b) {
    return arguments.length == 2 ? fn(a, b) : function(b) { fn(b, a) };
  }
}
```


### _get 만들어 좀 더 간단하게 하기
```javascript
function _get(obj, key) {
  return obj === null ? undefined : obj[key];
}

var user1 = users[0];
console.log(user1); // { id: 1, name: 'sujin }

console.log(_get(_user1, 'name'));
```

만약에 위의 코드에서 users[0] 이 name property를 가지고 있지 않으면 'name' of undefined 라고 에러가 뜨게 된다.

아래 _get 함수를 사용하게 되면 name property가 없어도 undefined type을 갖게되고 에러는 나지않는다.