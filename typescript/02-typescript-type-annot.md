# TypeScript (2) - Type Annotation 



## Type Annotation 
TypeScript는 유형 주석을 사용하여 변수, 함수, 객체 등과 같은 식별자의 유형을 명시적으로 지정합니다.

### 변수 및 상수의 유형 주석 
변수 및 상수에 대한 유형 주석을 지정하는 방법을 보여준다. 
```typescript
let variableName: type;
let variableName: type = value;
const constantName: type = value;
```

다음 예에서는 number 변수에 대한 주석을 사용한다. 
```typescript
let counter: number;
```
그 후에 counter 변수에 숫자만 할당할 수 있다. 


### 배열 유형
배열 유형에 주석을 추가하려면 특정 유형 다음에 대괄호를 사용합니다 
```typescript
let arrayName: type[];
```
```typescript
let names: string[] = ['John', 'Jane', 'Peter', 'David', 'Mary'];
```


### 객체 유형 
객체의 유형을 지정하려면 객체 유형 주석을 사용합니다. 예를 들어:
```typescript
let person: {
   name: string;
   age: number
};

person = {
   name: 'John',
   age: 25
}; // valid
```


### 함수 인수 및 반환 유형

다음은 매개변수 유형 주석 및 반환 유형 주석이 있는 함수 주석을 보여줍니다.

```typescript
let greeting : (name: string) => string;
```

이 예에서는 문자열을 받아들이고 greeting변수에 문자열을 반환하는 모든 함수를 할당할 수 있습니다 .

```typescript
greeting = function (name: string) {
    return `Hi ${name}`;
};
```

