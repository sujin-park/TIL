# 접기 - reduce

### reduce를 이용한 min, max 함수
```javascript

function _min(data) {
  return _reduce(data, (a, b) => {
      return a < b ? a : b;
  });
}

_min([1, 2, 4, 10, 5, -4]);


function _max(data) {
  return _reduce(data, (a, b) => {
      return a > b ? a : b;
  });
}

_max([1, 2, 4, 10, 5, -4]);

// min_by 와 max_by 는 보조함수를 같이 인자로 받기 때문에 첫번째 인자가
// 무엇이 들어와도 관계없다.

function _min_by(data, iter) {
  return _reduce(data, (a, b) => {
    return iter(a) < iter(b) ? a : b;
  })
}

function _max_by(data, iter) {
  return _reduce(data, (a, b) => {
    return iter(a) > iter(b) ? a : b;
  }) 
}

_min_by([1, 2, 4, 10, 5, -4], Math.abs); // 절대값으로 변경해서 min 숫자
_max_by([1, 2, 4, 10, 5, -4], Math.abs);

```