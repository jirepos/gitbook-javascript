# TypeScript (3) - Types


## Number 
**Number** 
```typescript
let price: number;
let price = 9.95;
```

**Decimal numbers**
```typescript
let counter: number = 0;
let x: number = 100, 
    y: number = 200;
```

**Binary Numbers**
```typescript
let bin = 0b100;
let anotherBin: number = 0B010;
```

**Octal Numbers**
```typescript
let octal: number = 0o10;
```

**Hexadecimal numbers**

```typescript
let hexadecimal: number = 0XA;
```

**Big Integers**
```typescript
let big: bigint = 9007199254740991n;
```



## String
JavaScript와 마찬가지로 TypeScript는 큰따옴표( ") 또는 작은따옴표( ')를 사용하여 문자열 리터럴을 묶습니다 .
```typescript
let firstName: string = 'John';
let title: string = "Web Developer";
```
다음 예는 백틱(`)을 사용하여 여러 줄 문자열을 만드는 방법을 보여줍니다.
```typescript
let description = `This TypeScript string can 
span multiple 
lines
`;
```


문자열 보간을 사용하면 다음과 같이 변수를 문자열에 포함할 수 있습니다.

```typescript
let firstName: string = `John`;
let title: string = `Web Developer`;
let profile: string = `I'm ${firstName}. 
I'm a ${title}`;

console.log(profile);
```
결과 
```shell
I'm John. 
I'm a Web Developer.
```


## Boolean

```typescript
let pending: boolean;
pending = true;
// after a while
// ..
pending = false;
```


## Object 
다음은 개체를 포함하는 변수를 선언하는 방법을 보여줍니다.

```typescript
let employee: object;

employee = {
    firstName: 'John',
    lastName: 'Doe',
    age: 25,
    jobTitle: 'Web Developer'
};

console.log(employee);
```


employee객체에 기본 값을 재할당 하면 오류가 발생합니다.

```typescript
employee = "Jane";
```
코드 언어:  JavaScript  ( javascript )

```shell
error TS2322: Type '"Jane"' is not assignable to type 'object'.
```


employee개체의 속성을 명시적으로 지정하려면 먼저 다음 구문을 사용하여 employee개체 를 선언 합니다.
```typescript
let employee: {
    firstName: string;
    lastName: string;
    age: number;
    jobTitle: string;
};
```
그런 다음 employee설명된 속성을 사용하여 리터럴 개체에 개체를 할당합니다 .
```typescript
employee = {
    firstName: 'John',
    lastName: 'Doe',
    age: 25,
    jobTitle: 'Web Developer'
};
```

또는 다음과 같이 동일한 명령문에서 두 구문을 결합할 수 있습니다.
```typescript
let employee: {
    firstName: string;
    lastName: string;
    age: number;
    jobTitle: string;
} = {
    firstName: 'John',
    lastName: 'Doe',
    age: 25,
    jobTitle: 'Web Developer'
};
```


**object vs. Object**
대문자 O로 시작하는 Object라고 불리는 다른 타입이 있다.  object type은 모든 non-primitive values를 의미하고, Object type는 모든 객체들의 기능을 설명한다. 예를 들어 Object 유형에는 모든 개체에서 액세스할 수 있는 toString()및 valueOf()메서드가 있습니다.


**빈 타입 {}**

빈 유형 {}은 자체 속성이 없는 개체를 설명합니다. 이러한 객체의 속성에 액세스하려고 하면 TypeScript에서 컴파일 시간 오류가 발생합니다.
```typescript
let vacant: {};
vacant.firstName = 'John';
```

오류
```shell
error TS2339: Property 'firstName' does not exist on type '{}'.
```
그러나 프로토타입 체인을Object 통해 객체에서 사용할 수 있는 유형에 선언된 모든 속성과 메서드에 액세스할 수 있습니다 .
```typescript
let vacant: {} = {};

console.log(vacant.toString());
```





## Array 
TypeScript array는 정렬된 데이터 목록입니다. 특정 유형의 값을 보유하는 배열을 선언하려면 다음 구문을 사용합니다.

```typescript
let arrayName: type[];
```
```typescript
let skills: string[];
```
배열에 하나 이상의 문자열을 추가할 수 있습니다.
```typescript
skills[0] = "Problem Solving";
skills[1] = "Programming";
```
또는 다음 push()방법을 사용하십시오 .
```typescript
skills.push('Software Design');
```

다음은 변수를 선언하고 문자열 배열을 할당합니다.
```typescript
let skills = ['Problem Sovling','Software Design','Programming'];
```

이 예에서 TypeScript 는skills 배열을 문자열 배열로 유추 합니다 . 다음과 동일합니다.
```typescript
let skills: string[];
skills = ['Problem Sovling','Software Design','Programming'];
```

TypeScript 배열은 JavaScript의 속성과 메서드에 액세스할 수 있습니다. 예를 들어 다음은 length 속성을 사용하여 배열의 요소 수를 가져옵니다.


```typescript
let series = [1, 2, 3];
console.log(series.length); // 3
```
그리고 forEach(), map(), reduce(), 와 같은 유용한 배열 방법을 모두 사용할 수 있습니다. 

```typescript
let series = [1, 2, 3];
let doubleIt = series.map(e => e* 2);
console.log(doubleIt);
```

**혼합 유형의 값 저장**

다음은 문자열과 숫자를 모두 포함하는 배열을 선언하는 방법을 보여줍니다.
```typescript
let scores = ['Programming', 5, 'Software Design', 4]; 
```
이 경우 TypeScript는 scores배열을 의 배열로 유추합니다 string | number.

다음과 동일합니다.

```typescript
let scores : (string | number)[];
scores = ['Programming', 5, 'Software Design', 4]; 
```


## Tuple 

튜플은 몇 가지 추가 고려 사항이 있는 배열 처럼 작동합니다 .

* 튜플의 요소 수는 고정되어 있습니다.
* 요소의 유형은 알려져 있으며 동일할 필요는 없습니다.


예를 들어, string과 number의 짝으로써 값을 표현하는 튜플을 사용할 수 있다. 
```typescript
let skill: [string, number];
skill = ['Programming', 5];
```

튜플에서 값의 순서는 중요합니다. skill 튜플의 값들의 순서를 [5, "Programming"]로 변경한다면 에러가 발생할 것이다. 


```typescript
let skill: [string, number];
skill = [5, 'Programming'];
```

예를 들어, 튜플을 사용하여 항상 3자리 패턴으로 제공되는 RGB 색상을 정의할 수 있습니다.
```typescript
(r,g,b)
```

```typescript
let color: [number, number, number] = [255, 0, 0];
```


**선택적 튜플 요소**

TypeScript 3.0부터 튜플은 물음표(?) 접미사를 사용하여 지정된 선택적 요소를 가질 수 있습니다.
예를 들어, 선택적 알파 채널 값을 사용하여 RGBA 튜플을 정의할 수 있습니다.


```typescript
let bgColor, headerColor: [number, number, number, number?];
bgColor = [0, 255, 255, 0.5];
headerColor = [0, 255, 255];
```






## Enum 
열거형은 명명된 상수 값의 그룹입니다. 열거형은 열거형을 나타냅니다.

열거형을 정의하려면 다음 단계를 따릅니다.
* 먼저 enum키워드 뒤에 열거형 이름을 사용합니다.
* 그런 다음 열거형에 대한 상수 값을 정의합니다.

다음은 열거형을 정의하기 위한 구문을 보여줍니다.


```typescript
enum name {constant1, constant2, ...};
```

다음 예에서는 연도를 나타내는 열거형을 만듭니다.

```typescript
enum Month {
    Jan,
    Feb,
    Mar,
    Apr,
    May,
    Jun,
    Jul,
    Aug,
    Sep,
    Oct,
    Nov,
    Dec
};
```


이 예에서 열거형 이름은 Month이고 상수 값은 Jan, Feb, Mar등입니다.
다음은 Month열거형을 month매개변수 유형으로 사용하는 함수를 선언합니다 .


```typescript
function isItSummer(month: Month) {
    let isSummer: boolean;
    switch (month) {
        case Month.Jun:
        case Month.Jul:
        case Month.Aug:
            isSummer = true;
            break;
        default:
            isSummer = false;
            break;
    }
    return isSummer;
}
```
그리고 다음과 같이 부를 수 있습니다.
```typescript
console.log(isItSummer(Month.Jun)); // true
```

코드에서 열거형으로 정의된 상수 값을 사용하는 것이 좋습니다.

그러나 다음 예제에서는 열거형 대신 숫자를 isItSummer()함수에 전달합니다. 그리고 그것은 작동합니다.


```typescript
console.log(isItSummer(6)); // true
```


**열거형 멤버의 번호 지정**
TypeScript는 열거형 정의에 나타나는 해당 멤버의 순서에 따라 열거형 멤버의 숫자 값을 정의합니다. 예를 들어, Jan0을 취하고 1을 Feb얻는 등입니다.

다음과 같이 열거형 멤버의 숫자를 명시적으로 지정할 수 있습니다.


```typescript
enum Month {
    Jan = 1,
    Feb,
    Mar,
    Apr,
    May,
    Jun,
    Jul,
    Aug,
    Sep,
    Oct,
    Nov,
    Dec
};
```

이 예에서 Jan상수 값은 0 대신 1을 Feb취 합니다. 는 2를 Mar취하고 3을 취하는 식입니다.

예를 들어 승인 상태에 열거형을 사용할 수 있습니다.

```typescript
enum ApprovalStatus {
    draft,
    submitted,
    approved,
    rejected
};
```
그런 다음 다음 ApprovalStatus과 같이 열거형을 사용할 수 있습니다 .
```typescript
const request =  {
    id: 1,
    status: ApprovalStatus.approved,
    description: 'Please approve this request'
};

if(request.status === ApprovalStatus.approved) {
    // send an email
    console.log('Send email to the Applicant...');
}
```


## Any 
때로는 변수에 값을 저장해야 할 수도 있습니다. 그러나 프로그램을 작성할 당시에는 그 유형을 모릅니다. 그리고 알 수 없는 값은 타사 API 또는 사용자 입력에서 올 수 있습니다.

이 경우 유형 검사를 옵트아웃하고 값이 컴파일 시간 검사를 통과하도록 허용하려고 합니다.

이렇게 하려면 any유형 을 사용합니다 . any유형은 변수에 어떤 유형의 값을 할당 할 수 있습니다 :



```typescript
// json may come from a third-party API
const json = `{"latitude": 10.11, "longitude":12.12}`;

// parse JSON to find location
const currentLocation = JSON.parse(json);
console.log(currentLocation);
```
이 예에서 currentLocation변수는 JSON.parse()함수에 의해 반환된 객체에 할당됩니다 .

그러나 currentLocation을 사용하여 객체 속성에 액세스하면 TypeScript도 검사를 수행하지 않습니다.

```typescript
console.log(currentLocation.x);
```
결과 
```shell
undefined
```

**TypeScript any: 암시적 입력**
유형을 지정하지 않고 변수를 선언하면 TypeScript는 사용자가 해당 any유형 을 사용한다고 가정합니다 . 이 기능을 유형 추론 이라고 합니다 . 기본적으로 TypeScript는 변수의 유형을 추측합니다.

```typescript
let result;
```
이 예에서 TypeScript는 유형을 유추합니다. 이 방법을 암시적 입력이라고 합니다.


**TypeScript any vs. object**

object유형이 있는 변수를 선언 하면 임의의 값을 할당할 수도 있습니다.
그러나 메소드가 실제로 존재하더라도 메소드를 호출할 수 없습니다



```typescript
let result: any;
result = 10.123;
console.log(result.toFixed());
result.willExist(); //
```

willExist() 메서드가 없다라도 컴파일 시에 어떠한 경고도 표시하지 않는다. willExist()가 runtime 시에 유효할 수도 있기 때문이다. 


그러나 result변수 유형을 로 변경 object하면 TypeScript 컴파일러에서 오류가 발생합니다.

```typescript
let result: object;
result = 10.123;
result.toFixed();
```
오류
```shell
error TS2339: Property 'toFixed' does not exist on type 'object'.
```



## Void 
일반적으로 void type은 어떤 값도 가지지 않는 것을 나타낸다.  any type의 반대와 비슷하다. 

일반정긍로 함수의 return type을 void를 사용하면 어떤 값도 반환하지 않는다. 

```typescript
function log(message): void {
    console.log(messsage);
}
```



## Union
때때로 숫자나 문자열인 매개변수를 기대하는 함수를 만나게 될 것입니다.
```typescript
function add(a: any, b: any) {
    if (typeof a === 'number' && typeof b === 'number') {
        return a + b;
    }
    if (typeof a === 'string' && typeof b === 'string') {
        return a.concat(b);
    }
    throw new Error('Parameters must be numbers or strings');
}
```
이 예에서 add()함수는 매개변수가 숫자인 경우 해당 매개변수의 합계를 계산합니다.

매개변수가 문자열인 경우 add()함수는 매개변수를 단일 문자열로 연결합니다. 

매개변수가 숫자나 문자열이 아니면 add()함수에서 오류가 발생합니다. 

add()함수 매개변수의 문제점은 매개변수에 any유형 이 있다는 것 입니다. 숫자도 문자열도 아닌 인수를 사용하여 함수를 호출할 수 있음을 의미합니다. TypeScript는 이에 대해 문제가 없습니다.


이 코드는 성공적으로 컴파일되지만 런타임에 오류가 발생합니다.


```typescript
add(true, false);
```
이를 해결하기 위해 TypeScript 공용체 유형을 사용할 수 있습니다. 공용체 유형을 사용하면 여러 유형을 하나의 유형으로 결합할 수 있습니다.

예를 들어, 다음 변수는 number또는  string 유형입니다.


```typescript
let result: number | string;
result = 10; // OK
result = 'Hi'; // also OK
result = false; // a boolean value, not OK
```

공용체 유형은 두 가지 유형이 아닌 여러 유형 중 하나일 수 있는 값을 설명합니다. 예를 들어 number | string | boolean숫자, 문자열 또는 부울이 될 수 있는 값의 유형입니다.


add()함수 예제로 돌아가서 매개변수 유형을 다음 any과 같이 공용체 에서 변경할 수 있습니다.


```typescript
function add(a: number | string, b: number | string) {
    if (typeof a === 'number' && typeof b === 'number') {
        return a + b;
    }
    if (typeof a === 'string' && typeof b === 'string') {
        return a.concat(b);
    }
    throw new Error('Parameters must be numbers or strings');
}
```


## Type alias 
유형 별칭을 사용하면 기존 유형에 대한 새 이름을 만들 수 있습니다. 다음은 유형 별칭의 구문을 보여줍니다.


```typescript
type alias = existingType;
```
기존 유형은 모든 유효한 TypeScript 유형일 수 있습니다.

다음 예제에서는 문자열 유형에 대해 유형 별칭 chars를 사용합니다.


```typescript
type chars = string;
let messsage: chars; // same as string type
```


공용체 유형에 대한 유형 별명을 작성하는 것이 유용합니다. 예를 들어:


```typescript
type alphanumeric = string | number;
let input: alphanumeric;
input = 100; // valid
input = 'Hi'; // valid
input = false; // Compiler error
```



## String
문자열 리터럴 유형을 사용하면 지정된 문자열 리터럴을 하나만 허용하는 유형을 정의할 수 있습니다.


```typescript
let click: 'click';
```


리터럴 문자열 click에 'click'을  할당하면 다음 click과 같이 유효합니다.



```typescript
click = 'click'; // valid
```
그러나 다른 문자열 리터럴을 에 할당 click하면 TypeScript 컴파일러에서 오류가 발생합니다

```typescript
click = 'dblclick'; // compiler error
```





문자열 리터럴 유형은 공용체 유형 과 잘 결합 되어 변수에 대한 유한한 문자열 리터럴 값 집합을 정의 할 수 있습니다 .

```typescript
let mouseEvent: 'click' | 'dblclick' | 'mouseup' | 'mousedown';
mouseEvent = 'click'; // valid
mouseEvent = 'dblclick'; // valid
mouseEvent = 'mouseup'; // valid
mouseEvent = 'mousedown'; // valid
mouseEvent = 'mouseover'; // compiler error
```


여러 위치에서 문자열 리터럴 유형을 사용하면 매우 장황해질 것입니다.
이를 방지하기 위해 유형 별칭을 사용할 수 있습니다. 
```typescript
type MouseEvent: 'click' | 'dblclick' | 'mouseup' | 'mousedown';
let mouseEvent: MouseEvent;
mouseEvent = 'click'; // valid
mouseEvent = 'dblclick'; // valid
mouseEvent = 'mouseup'; // valid
mouseEvent = 'mousedown'; // valid
mouseEvent = 'mouseover'; // compiler error

let anotherEvent: MouseEvent;
```


