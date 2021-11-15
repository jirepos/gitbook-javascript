# 구조 분할 

## 배열 구조 분할 
배열을 분할 할 수 있다. 
```javascript
    // 배열 구조 분해 
    var foo = ["one", "two", "three"];

    var [red, yellow, green] = foo;
    console.log(red); // "one"
    console.log(yellow); // "two"
    console.log(green); // "three"
```



## 객체 구조 분할 
객체를 변수로 분할 할 수 있다. 
```javascript
    // 객체 구조 분할 
    var user = {
      name: "홍길동",
      age: 10
    }
    let { name, age } = user;
    console.log(name);
    console.log(age);

```

## 함수 구조 분할 
함수가 반환한 객체를 분할 할 수 있다. 
```javascript
    // 함수 구조 분할 
    function getSomtehing() {
      let add = 1 + 2;
      let multi = 2 * 10;
      return { add, multi }
    }
    let { add, multi } = getSomtehing();
    console.log(add);
    console.log(multi);

```
배열로 반환한 값을 분할 할 수 있다. 

```javascript
    // 배열로 반환 
    function returnArray() {
      let add = 1 + 2;
      let multi = 2 * 10;
      return [add, multi]
    }
    let [resAdd, resMulti] = returnArray();
    console.log(resAdd);
    console.log(resMulti);
```




## 전개 연산자(...)

전개 연산자( ... )를 사용하여 좌항에서 명시적으로 할당되지 않은 나머지 배열 값들을 사용할 수 있다. 

### 배열

```jsx
[a1, a2, ...rest_a] = [1, 2, 3, 4, 5, 6, 7, 8, 9];
console.log(a1); // 1
console.log(a2); // 2
console.log(rest_a); // [3, 4, 5, 6, 7, 8, 9]
```

### 객체

```jsx
var { a1, a2, ...rest_a } = { a1 : 10, a2 : 20, a3 : 30, a4 : 40 };
console.log(a1); // 10
console.log(a2); // 20
console.log(rest_a); // { a3: 30, a4: 40 }
```

## 복사

### 기본 복사

copy1은 **arr을 참조하기 때문에 0 번 요소가 변경**이 된다. 

```jsx
var arr = [1,2,3];
var copy1 = arr;
arr[0] = 'String';
console.log(arr); // [ 'String', 2, 3 ]
```

### 깊은 복사

copy2와 copy3는 깊은 복사를 하기 때문에 0 번 요소가 변경되었어도 반영이 되지 않는다.

```jsx
var arr = [1,2,3];
var [...copy2] = arr;
var copy3 = [...arr];
arr[0] = 'String';
console.log(copy2); // [ 1, 2, 3 ]
console.log(copy3); // [ 1, 2, 3 ]
```

### 객체 복사

전개 연산자를 사용하여 객체를 복사하면서도 새로운 값을 줄 수 있다. 

```jsx
var prevObj = {
  name: "Hong",
  birth: "2021-11-01",
  age: 10
};

var state = {
  ...prevObj,
  age: 23  // age 값만 변경이 된다.
};

console.log(state); // { name: 'Hong', birth: '2021-11-01', age: 23 }
```

### 함수에서 사용

함수의; 파라미터에서도 비 구조화 할당을 사용할 수 있다. 

```jsx
function renderUser({name, age, addr}) {
  console.log(name);
  console.log(age);
  console.log(addr);
}

var user = { name: "Hong", age: 20, addr: "Seoul"}
renderUser(user);  
```