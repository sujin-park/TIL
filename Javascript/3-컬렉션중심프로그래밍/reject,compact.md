### reject, compact

거르기

```
console.log(
  _filter(users, user => user.age > 30)
)

function _negate(func) {
  return function (value) {
    return !func(value);
  }
}

1. reject

function _reject(data, predi) {
  return _filter(data, _negate(predi));
}

// user.age 가 30세 이상인 값은 제외
console.log(
  _reject(users, user => user.age > 30)
)

2. compact

const _compact = _filter(_identity);

console.log(_compact([1, 2, 0, false, null, {}])); // 1, 2, {}
```
