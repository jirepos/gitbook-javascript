# TypeScript

## 익명함수

가볍게 파라미터를 그대로 반환하는 함수를 사용해 보겠다.

```javascript
let func = x => { return x; };
console.log(func(1));
```

다음과 같이 작성해도 된다.

```javascript
let func = x =>  x;
console.log(func(1));
```

익명 함수 사용시 가독성을 위해서 type 선언자 를 통해서 익명 함수의 형태를 지정할 수도 있다.

```javascript
type mytype = (x:number) => number; 
let ex: mytype = (x: number) => x; 
console.log(ex(1));
```

익명 함수를 만든 다음 바로 실행할 수도 있다.

```javascript
let result = ( (x:number) => x)(3);
console.log(result);
```

## 콜백함수

```javascript
type mytype = (x:string) => string; 
let ex: mytype = (x: string) => x; 

function callfunc(msg:string, func: mytype) {
    return func(msg);
}

let res = callfunc("hello", ex);
console.log(res);
```
