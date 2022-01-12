# TypeScript (4) - Functions



## 함수 소개 


JavaScript와 마찬가지로 function키워드를 사용하여 TypeScript에서 함수를 선언합니다.

```typescript
function name(parameter: type, parameter:type,...): returnType {
   // do something
}
```

JavaScript와 달리 TypeScript를 사용하면 매개변수에 유형 주석 을 사용 하고 함수의 값을 반환할 수 있습니다.

다음 add()함수 예를 보겠습니다.
```typescript
function add(a: number, b: number): number {
    return a + b;
}
```


이 예에서 add()함수는 number유형 이 있는 두 개의 매개변수를 허용 합니다.

add()함수 를 호출할 때 TypeScript 컴파일러는 함수에 전달된 각 인수가 숫자인지 확인합니다.

에서 add()기능 예를 들어, 당신은 단지, 그것으로 다른 유형의없는 값을 숫자를 전달할 수 있습니다.

다음 코드는 add()함수 에 두 개의 숫자 대신 두 개의 문자열을 전달하기 때문에 오류가 발생 합니다.


```typescript
let sum = add('10', '20');
```

수가 값을 반환하지 않으면 해당 void유형을 반환 유형으로 사용할 수 있습니다 . void키워드는 함수가 값을 반환하지 않음을 나타냅니다. 



```typescript
function echo(message: string): void {
    console.log(message.toUpperCase());
}
```



## 함수 유형 
함수 유형에는 매개변수와 반환 유형의 두 부분이 있습니다. 함수 유형을 선언할 때 다음 구문으로 두 부분을 모두 지정해야 합니다.


```typescript
(parameter: type, parameter:type,...) => type
```


다음 예제는 두 개의 숫자를 받아들이고 숫자를 반환하는 함수 유형을 가진 변수를 선언하는 방법을 보여줍니다.

```typescript
let add: (x: number, y: number) => number;
```



다음 예에서는 add변수에 함수를 할당하는 방법을 보여줍니다 .


```typescript
add = function (x: number, y: number) {
    return x + y;
};
```
또한 다음과 같이 변수를 선언하고 변수에 함수를 할당할 수 있습니다.


```typescript
let add: (a: number, b: number) => number =
    function (x: number, y: number) {
        return x + y;
    };
```


## Optional Parameters



JavaScript에서는 함수가 매개변수를 지정하더라도 인수를 전달하지 않고 함수를 호출할 수 있습니다. 따라서 JaveScript는 기본적으로 선택적 매개변수를 지원합니다.

TypeScript에서 컴파일러는 다음과 같은 경우 모든 함수 호출을 확인하고 오류를 발생시킵니다.

인수의 수가 함수에 지정된 매개변수의 수와 다릅니다.
또는 인수 유형이 함수 매개변수 유형과 호환되지 않습니다.


함수 매개변수를 선택사항으로 만들려면 ?매개변수 이름 뒤에 사용합니다 .


```typescript
function multiply(a: number, b: number, c?: number): number {

    if (typeof c !== 'undefined') {
        return a * b * c;
    }
    return a * b;
}
```


선택적 매개변수는 매개변수 목록에서 필수 매개변수 뒤에 나타나야 합니다.

예를 들어 b매개변수를 선택사항으로 만들고 c매개변수가 필수인 경우 TypeScript 컴파일러에서 오류가 발생합니다.


```typescript
function multiply(a: number, b?: number, c: number): number {

    if (typeof c !== 'undefined') {
        return a * b * c;
    }
    return a * b;
}
```
오류:
```shell
error TS1016: A required parameter cannot follow an optional parameter.
```

## Default Parameters
JavaScript 는 다음 구문을 사용하여 ES2015(또는 ES6)부터 기본 매개변수를 지원했습니다 

```typescript
function name(parameter1=defaultValue1,...) {
   // do something
}
```
JavaScript와 유사하게 TypeScript에서 동일한 구문으로 기본 매개변수를 사용할 수 있습니다.

```typescript
function name(parameter1:type=defaultvalue1, parameter2:type=defaultvalue2,...) {
   //
}
```

```typescript
function applyDiscount(price: number, discount: number = 0.05): number {
    return price * (1 - discount);
}

console.log(applyDiscount(100)); // 95
```

**기본 매개변수 및 선택적 매개변수**



선택적 매개변수 와 마찬가지로 기본 매개변수도 선택사항입니다. 즉, 함수를 호출할 때 기본 매개변수를 생략할 수 있습니다.

또한 기본 매개변수와 후행 기본 매개변수는 모두 동일한 유형을 공유합니다.


```typescript
function applyDiscount(price: number, discount: number = 0.05): number {
  // ...
}
```
그리고
```typescript
function applyDiscount(price: number, discount?: number): number {
  // ...
}
```



## Rest parameters
이 튜토리얼에서는 무한한 수의 인수를 배열로 나타낼 수 있는 TypeScript rest 매개변수에 대해 배웁니다.


rest 매개변수를 사용하면 함수가 지정된 유형의 0개 이상의 인수를 허용할 수 있습니다. TypeScript에서 나머지 매개변수는 다음 규칙을 따릅니다.

* 함수에는 하나의 나머지 매개변수만 있습니다.
* 나머지 매개변수는 매개변수 목록의 마지막에 나타납니다.
* 나머지 매개변수의 유형은 배열 유형 입니다.


나머지 매개변수를 선언하려면 매개변수 이름에 세 개의 점을 접두어로 붙이고 배열 유형을 유형 주석으로 사용합니다.


```typescript
function fn(...rest: type[]) {
   //...
}
```
다음 예에서는 나머지 매개변수를 사용하는 방법을 보여줍니다.

```typescript
function getTotal(...numbers: number[]): number {
    let total = 0;
    numbers.forEach((num) => total += num);
    return total;
}
```

이 예에서 getTotal()전달된 숫자의 총계를 계산합니다.

숫자 매개변수는 나머지 매개변수이므로 하나 이상의 숫자를 전달하여 합계를 계산할 수 있습니다.


```typescript
console.log(getTotal()); // 0
console.log(getTotal(10, 20)); // 30
console.log(getTotal(10, 20, 30)); // 60
```



## Function Overloadings
TypeScript에서 함수 오버로딩을 사용하면 매개변수 유형과 함수의 결과 유형 간의 관계를 설정할 수 있습니다

> TypeScript 함수 오버로딩은 C# 및 Java와 같은 다른 정적으로 유형이 지정된 언어에서 지원하는 함수 오버로딩과 다릅니다.

> 나중에 정리하기로 한다. 



