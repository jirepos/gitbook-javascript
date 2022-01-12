# TypeScript (6) - Interfaces

## 소개 


TypeScript 인터페이스는 코드 내에서 계약을 정의합니다. 또한 유형 검사를 위한 명시적 이름을 제공합니다.

간단한 예부터 시작하겠습니다.


```typescript
function getFullName(person: {
    firstName: string;
    lastName: string
}) {
    return `${person.firstName} ${person.lastName}`;
}

let person = {
    firstName: 'John',
    lastName: 'Doe'
};

console.log(getFullName(person));
```

이 예에서 TypeScript 컴파일러는 getFullName()함수에 전달하는 인수를 확인합니다 .

인수에 유형이 문자열인 두 개의 속성이 있는 경우 TypeScript 컴파일러는 검사를 통과합니다. 그렇지 않으면 오류가 발생합니다.

코드에서 분명히 알 수 있듯이 함수 인수 의 유형 주석은 코드를 읽기 어렵게 만듭니다.

이를 해결하기 위해 TypeScript는 인터페이스의 개념을 도입합니다.

다음 Person은 두 개의 문자열 속성이 있는 라는 인터페이스를 사용합니다 .


```typescript
interface Person {
    firstName: string;
    lastName: string;
}
```
관례에 따라 인터페이스 이름은 낙타 대소문자를 사용합니다. 그들은 이름의 단어를 구분하기 위해 단일 대문자를 사용합니다. 예를 들어, Person, UserProfile및 FullName.


Person인터페이스를 정의한 후 유형으로 사용할 수 있습니다. 그리고 인터페이스 이름으로 함수 매개변수에 주석을 달 수 있습니다.


```typescript
function getFullName(person: Person) {
    return `${person.firstName} ${person.lastName}`;
}

let john = {
    firstName: 'John',
    lastName: 'Doe'
};

console.log(getFullName(john));
```


## 선택적 속성

인터페이스에는 선택적 속성이 있을 수 있습니다. 선택적 속성을 선언하려면 다음과 같이 선언의 속성 이름 끝에 물음표 ?를 사용합니다. 

```typescript
interface Person {
    firstName: string;
    middleName?: string;
    lastName: string;
}
```


이 예에서 Person인터페이스에는 두 개의 필수 속성과 하나의 선택적 속성이 있습니다.

그리고 다음은 함수 에서 Person인터페이스 를 사용하는 방법을 보여줍니다


```typescript
function getFullName(person: Person) {
    if (person.middleName) {
        return `${person.firstName} ${person.middleName} ${person.lastName}`;
    }
    return `${person.firstName} ${person.lastName}`;
}
```



## 읽기 전용 속성
객체가 처음 생성될 때만 속성을 수정할 수 있어야 하는 경우 속성 readonly이름 앞에 키워드를 사용할 수 있습니다 .
```typescript
interface Person {
    readonly ssn: string;
    firstName: string;
    lastName: string;    
}

let person: Person;
person = {
    ssn: '171-28-0926',
    firstName: 'John',
    lastName: 'Doe'
}
```
이 예에서는 ssn속성을 변경할 수 없습니다.
```typescript
person.ssn = '171-28-0000';
```


## 함수 유형
속성을 사용하여 개체를 설명하는 것 외에도 인터페이스를 사용하면 함수 유형 을 설명할 수도 있습니다 .

함수 유형을 설명하려면 유형 및 반환 유형이 있는 매개변수 목록을 포함하는 함수 서명에 인터페이스를 할당합니다.


```typescript
interface StringFormat {
    (str: string, isUpper: boolean): string
}
```


이제 이 함수 유형 인터페이스를 사용할 수 있습니다.

다음은 함수 유형의 변수를 선언하고 동일한 유형의 함수 값을 할당하는 방법을 보여줍니다.

```typescript
let format: StringFormat;

format = function (str: string, isUpper: boolean) {
    return isUpper ? str.toLocaleUpperCase() : str.toLocaleLowerCase();
};

console.log(format('hi', true));
```
매개변수 이름은 함수 서명과 일치할 필요가 없습니다. 다음 예는 위의 예와 동일합니다.

```typescript
let format: StringFormat;

format = function (src: string, upper: boolean) {
    return upper ? src.toLocaleUpperCase() : src.toLocaleLowerCase();
};

console.log(format('hi', true));
```

StringFromat는 요구되는 string, boolean 아규먼트들을 전달한다는 것을 보장한다. 하지만 아래 또한 동작한다. 

```typescript
let lowerCase: StringFormat;
lowerCase = function (str: string) {
    return str.toLowerCase();
}

console.log(lowerCase('Hi', false));
```



## Class Types
Java 또는 C#으로 작업한 경우 인터페이스의 주요 용도가 관련 없는 클래스 간의 계약을 정의하는 것임을 알 수 있습니다.

예를 들어 다음 Json인터페이스는 관련 없는 클래스에서 구현할 수 있습니다.


```typescript
interface Json {
   toJSON(): string
}
```
다음은 Json인터페이스 를 구현하는 클래스를 선언합니다 .

```typescript
class Person implements Json {
    constructor(private firstName: string,
        private lastName: string) {
    }
    toJson(): string {
        return JSON.stringify(this);
    }
}

```

다음 예제에서는 Person클래스 를 사용하는 방법을 보여줍니다 .


```typescript
let person = new Person('John', 'Doe');
console.log(person.toJson());
```


## 하나의 인터페이스를 확장하기 

두가지 메서드를 가지는 Mailable이라는 인터페이스가 있다고 가정한다.
```typescript
interface Mailable {
    send(email: string): boolean
    queue(email: string): boolean
}
```

이미 Mailable 인터페이스를 구현한 많은 클래스들이 있다. 

이제 Mailable 인터페이스에 새로운 메서드를 추가하기를 원할 수 있다. 

```typescript
later(email: string, after: number): void
```


그러나 인터페이스에 later()메서드를 추가 Mailable하면 현재 코드가 깨집니다.


이를 피하기 위해 Mailable 인터페이스를 확장하는 새 인터페이스를 만들 수 있습니다 .


```typescript
interface FutureMailable extends Mailable {
    later(email: string, after: number): boolean
}
```

인터페이스를 확장하려면 extends다음 구문과 함께 키워드 를 사용 합니다.
```typescript
interface A {
    a(): void
}

interface B extends A {
    b(): void
}

```

다음은 FutureMailable인터페이스 를 구현하는 방법을 보여줍니다 .


```typescript
class Mail implements FutureMailable {
    later(email: string, after: number): boolean {
        console.log(`Send email to ${email} in ${after} ms.`);
        return true;
    }
    send(email: string): boolean {
        console.log(`Sent email to ${email} after ${after} ms. `);
        return true;
    }
    queue(email: string): boolean {
        console.log(`Queue an email to ${email}.`);
        return true;
    }
}
```


## 여러 인터페이스를 확장하는 인터페이스

인터페이스는 여러 인터페이스를 확장하여 모든 인터페이스의 조합을 생성할 수 있습니다.

```typescript
interface C {
    c(): void
}

interface D extends B, C {
    d(): void
}

```



## 클래스를 확장하는 인터페이스

TypeScript를 사용하면 인터페이스에서 클래스를 확장할 수 있습니다. 이 경우 인터페이스는 클래스의 속성과 메서드를 상속합니다. 또한 인터페이스는 공용 멤버뿐만 아니라 클래스의 private 및 protected 멤버를 상속할 수 있습니다.


이는 인터페이스가 private 또는 protected 멤버가 있는 클래스를 확장할 때 인터페이스가 확장되는 해당 클래스의 하위 클래스 또는 해당 클래스에 의해서만 인터페이스를 구현할 수 있음을 의미합니다



```typescript
class Control {
    private state: boolean;
}

// 클래스를 상속하여 인터페이스를 선언 
interface StatefulControl extends Control {
    enable(): void
}

// 인터페이스를 구현 
class Button extends Control implements StatefulControl {
    enable() { }
}

// 인터페이스 구현 및 클래스 상속 
class TextBox extends Control implements StatefulControl {
    enable() { }
}
// 클래스 상속
class Label extends Control { }


// Error: cannot implement
class Chart implements StatefulControl {
    enable() { }

}
```


