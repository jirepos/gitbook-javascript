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



