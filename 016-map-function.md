# map 함수
map() 메서드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환합니다.

**즉, 배열을 넘기면 하나 하나 실행하여 그 결과를 다시 배열로 만든다.** 

map() 함수에 배열  array1을 넘기면  배열 요소 하나 하나를  map 함수의 callback 함수 (x ⇒ x * 2)에게 넘기고 그 결과를 다시 배열로 만든다.  결과 값은 배열 요소에 2를 곱한 요소들을 가진 배열이 리턴된다.

```jsx

const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

위 식은 다음과 같이  function을 사용하여 표시할 수 있다. 

```jsx
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(function(x)  { return x* 2});

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

## map을 활용하여 배열 속 객체를 재구성하기

map 함수를 사용하여 kvArray 객체 배열을 다른 형태의 객체 배열로 구성하여 반환한다. 

```jsx
var kvArray = [{key:1, value:10},
  {key:2, value:20},
  {key:3, value: 30}];

var reformattedArray = kvArray.map(function(obj) {
    var rObj = {};
    rObj[obj.key] = obj.value;
    return rObj;
  });

console.log(reformattedArray)   // reformattedArray는 [{1:10}, {2:20}, {3:30}]

// reformattedArray는 [{1:10}, {2:20}, {3:30}]
// kvArray는 그대로
// [{key:1, value:10},
//  {key:2, value:20},
//  {key:3, value: 30}]
```