# Arrow Function

## 객체 반환

객체를 반환해 보자. 다음은  {  a: 1}을 반환한다. 

```jsx
() => { return { a: 1 }; }
```

함수를 사용해 보자.  콘솔에 1이 출력될 것이다. 

```jsx
const param = () => ({ a: 1 })
console.log(param().a);  // 1 

```

위 함수 정의는 return 문이 없어도 가능하다. 

```jsx
() => { return { a: 1 }; }
() => ({ a: 1 })  // 위 표현과 동일하다. 객체 반환시 소괄호를 사용한다.
```

## 파라미터가 있는 함수

파라미터가 있는 익명 함수를 선언한다.

```jsx
const template = (arg) => ( {
  user: arg.name // 객체의 name 속성의 값을 user에 할당
})

```

객체를 파라미터로 넘긴다. 

```jsx
var retval = template({ name: "kim"})
```

값을 출력해 보자. 

```jsx
console.log(retval.user)  // kim
```

## bind()

모든 함수는 `this`를 수정하게 해주는 내장 메서드 [bind](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)를 제공한다. 기본 문법은 다음과 같다. 

```jsx
let user = {
  firstName: "John"
};

function func() {
  alert(this.firstName);
}

let funcUser = func.bind(user);
funcUser(); // John
```

[https://ko.javascript.info/bind](https://ko.javascript.info/bind)