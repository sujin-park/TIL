# 찾아내기

### find 만들기
```javascript
function _find(list, predi) {
  const keys = _keys(list);
  for (let i = 0; i < keys.length; i++) {
    const val = list[keys[i]];
    if (predi(val)) return predi(val);
  }
}

* 사용법 (필터와 다르게 일치하는 값 1개만 return 해줌)
console.log(
  _find(users, user => user.id === 20) // 일치하는 Object
)
```

### find_index
```javascript
function _find_index(list, predi) {
  const keys = _keys(list);
  for (let i = 0; i < keys.length; i++) {
    if (predi(list[keys[i]])) return i;
  }
  return -1;
}

console.log(
  _find_index(users, user => user.id === 20) // 일치하는 인덱스 : 1
)
```

### some

```javascript
function _some(data, predi) {
  return _find_index(data, predi || _identity) != -1;
}

_some([1, 2, 5, 10, 20], value => value > 10); // true

_some([null, false, 1]) // false
```

### every
```javascript
function _some(data, predi) {
  return _find_index(data, _negate(predi || _identity)) != -1;
}

_every_([1, 2, 5, 10, 20], value => value > 10); // false
```