### 컬렉션 중심 프로그래밍의 4가지 유형과 함수

가장 앞에 있는 함수들이 추상화 레벨이 높아서 대표적인 함수라고 할 수 있다.

---
1. 수집하기 - map, values, pluck 등
2. 거르기 - filter, reject, compact, without 등 
3. 찾아내기 - find, some, every 등
4. 접기, 축약 - reduce, min, max, group_by, count_by
---

#### 수집하기 - map
 
```javascript
console.log(
  _map(users, function(user) {
    return user.name;
  })
)
```

1. values
key, value 로 되어있는 데이터에는 values가 유의미하다.
```javascript
let _values = _map(_identity);

function _identity (val) {
  return val;
}

let a = 10;
console.log(_identity(a)); // 10

console.log(_values(users[0])); // ["1", "2", "3"]
console.log(_map(_identity)(users[0])); // curryr로 map이 만들어져 있기 때문에 평가순서를 뒤집을 수 있다.
```

2. pluck

```javascript
function _pluck (data, key) {
  return _map(data, _get(key));
}

console.log(_pluck(users, 'age')); // [33, 22, 11, ...]
```
