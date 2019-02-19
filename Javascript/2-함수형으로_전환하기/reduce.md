# reduce 함수 만들기

```javascript
/* @params list, iter, memo
  두번째의 iter 함수를 재귀적으로 호출하면서 첫번째 인자값 -> 하나의 값으로 축약해 나가게 하는 함수
*/
function _reduce (list, iter, memo) {
  _each(list, (val) => {
    memo = iter(memo, val)
  })
  return memo
}

/* reduce 함수 기본 사용 예제 */
_reduce([1, 2, 3], (a, b) => {
  return a + b;
}, 10); // 16

/* iter 함수를 add 함수라고 가정했을 때 */
const add = function (a, b) {
  return a + b
}

/* reduce 함수의 작동 과정 */
memo = add(0, 1)
memo = add(memo, 2)
memo = add(memo, 3)
return memo

/* reduce 함수 인자값 두개만 보낼 때 구현 방법*/

function _reduce (list, iter, memo) {
  if (arguments.length === 2) {
    memo = list[0]
    list = Array.prototype.slice.call(list, 1) // array와 array like가 와도 할 수 있도록 사용
  }
  _each(list, (val) => {
    memo = iter(memo, val)
  })
  return memo
}

_reduce([1, 2, 3], add)

```