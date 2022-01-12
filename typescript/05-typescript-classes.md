# TypeScript (5) - Classes



## 클래스 소개


JavaScript에는 Java 및 C#과 같은 다른 프로그래밍 언어와 같은 클래스 개념이 없습니다. ES5에서는 생성자 함수와 프로토타입 상속 을 사용하여 "클래스"를 만들 수 있습니다.

예를 들어, Personssn, 이름 및 성의 세 가지 속성이 있는 클래스 를 만들려면 다음 생성자 함수를 사용합니다.


```jsx
function Person(ssn, firstName, lastName) {
    this.ssn = ssn;
    this.firstName = firstName;
    this.lastName = lastName;
}
```


다음으로 다음과 같이 이름과 성을 연결하여 사람의 전체 이름을 가져오는 프로토타입 메서드를 정의할 수 있습니다.

```jsx
Person.prototype.getFullName = function () {
    return `${this.firstName} ${this.lastName}`;
}
```


그런 다음 새 객체를 만들어 Person "클래스"를 사용할 수 있습니다.
```jsx
let person = new Person('171-28-0926','John','Doe');
console.log(person.getFullName());
```


ES6을 사용하면 생성자 함수와 프로토타입 상속을 생성하기 위한 단순한 구문 설탕인 클래스를 정의할 수 있습니다 .

```jsx
class Person {
    ssn;
    firstName;
    lastName;

    constructor(ssn, firstName, lastName) {
        this.ssn = ssn;
        this.firstName = firstName;
        this.lastName = lastName;
    }
}
```

클래스 구문에서 생성자는 명확하게 정의되어 클래스 내부에 배치됩니다. 다음은 getFullName()메서드를 추가합니다 

```jsx
class Person {
    ssn;
    firstName;
    lastName;

    constructor(ssn, firstName, lastName) {
        this.ssn = ssn;
        this.firstName = firstName;
        this.lastName = lastName;
    }

    getFullName() {
        return `${this.firstName} ${this.lastName}`;
    }
}
```
Person클래스를 사용하는 것은 Person생성자 함수 와 동일 합니다.


```jsx
let person = new Person('171-28-0926','John','Doe');
console.log(person.getFullName());
```


TypeScript 클래스는 클래스 의 속성과 메서드에 유형 주석 을 추가 합니다 . 다음은 Person TypeScript 의 클래스를 보여줍니다 .


```typescript
class Person {
    ssn: string;
    firstName: string;
    lastName: string;

    constructor(ssn: string, firstName: string, lastName: string) {
        this.ssn = ssn;
        this.firstName = firstName;
        this.lastName = lastName;
    }

    getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
}
```

속성, 생성자 및 메서드에 유형에 주석을 추가하면 TypeScript 컴파일러는 해당 유형 검사를 수행합니다.

예를 들어 ssna로 초기화할 수 없습니다 number. 다음 코드는 오류를 발생시킵니다.

```typescript
let person = new Person(171280926, 'John', 'Doe');
```


## Access Modifiers


액세스 한정자는 클래스 의 속성과 메서드의 가시성을 변경합니다 . TypeScript는 세 가지 액세스 한정자를 제공합니다.

* private
* protected
* public


### private 


private속성이나 메서드에 한정자를 추가 하면 동일한 클래스 내에서 해당 속성이나 메서드에 액세스할 수 있습니다. 클래스 외부의 private 속성이나 메서드에 액세스하려고 하면 컴파일 시간에 오류가 발생합니다.

```typescript
class Person {
    private ssn: string;
    private firstName: string;
    private lastName: string;
    // ...
}
```

private속성이 준비 되면 클래스 ssn의 생성자 또는 메서드에서 속성에 액세스할 수 있습니다

```typescript
class Person {
    private ssn: string;
    private firstName: string;
    private lastName: string;

    constructor(ssn: string, firstName: string, lastName: string) {
        this.ssn = ssn;
        this.firstName = firstName;
        this.lastName = lastName;
    }

    getFullName(): string {
        return `${this.firstName} ${this.lastName}`; 
    }
}
```



### public 
public 한정자를 사용하면 모든 위치에서 클래스 속성과 메서드에 액세스할 수 있습니다. 속성 및 메서드에 대한 액세스 한정자를 지정하지 않으면 기본적으로 public 한정자를 사용합니다.


```typescript
class Person {
    // ...
    public getFullName(): string {
        return `${this.firstName} ${this.lastName}`; 
    }
    // ...
}
```



### protected
protected modifier는 클래스의 속성 및 메소드는 동일한 클래스 내의 서브 클래스 내에서 접근하고있을 수 있다.


클래스(자식 클래스)가 다른 클래스(상위 클래스)로부터 상속받는 경우, 이는 상위 클래스의 하위 클래스입니다.

다른 곳에서 보호된 속성이나 메서드에 액세스하려고 하면 TypeScript 컴파일러에서 오류가 발생합니다.


속성이나 메서드에 protected 한정자를 추가하려면 protected키워드 를 사용합니다 . 

```typescript
class Person {

    protected ssn: string;
    
    // other code
}

```

ssn속성은 이제 보호됩니다. Person클래스 내에서 그리고 클래스에서 상속된 모든 클래스에서 액세스할 수 있습니다 Person. 여기에서 상속에 대해 자세히 알아볼 것입니다.



Person 클래스는 두 개의 개인 특성과 한 보호 속성을 선언합니다. 생성자는 이러한 속성을 3개의 인수로 초기화합니다. 

코드를 더 짧게 만들기 위해 TypeScript를 사용하면 다음과 같이 생성자에서 속성을 선언하고 초기화할 수 있습니다.

```typescript
class Person {
    constructor(protected ssn: string, private firstName: string, private lastName: string) {
        this.ssn = ssn;
        this.firstName = firstName;
        this.lastName = lastName;
    }

    getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
}
```



**요약**

* 타입스크립트는 클래스의 메서드와 속성에 대한 세 가지 접근 수정을 제공합니다 private, protected하고 public.
* private수정은 같은 클래스 내에서 액세스 할 수 있습니다.
* protected수정은 같은 클래스와 서브 클래스 내에서 액세스 할 수 있습니다.
* public개질제는 모든 위치에서 액세스를 허용한다.








## Gettes/Setters


다음은 age,firstName,lastName  세가지 속성을 갖는 간단한 Person 클래스를 보여줍니다 .



```typescript
class Person {
    public age: number;
    public firstName: string;
    public lastName: string;
}
```

Person클래스의 속성에 액세스하려면 다음과 같이 하면 됩니다.


```typescript
let person = new Person();
person.age = 26;
```




사용자 입력에서 가져온 값을 age속성에 할당한다고 가정합니다 .
```typescript
person.age = inputAge;
```

inputAge 모든 숫자가 될 수 있습니다. 연령의 유효성을 확인하기 위해 다음과 같이 배정 전에 수표를 휴대할 수 있습니다.

```typescript
if( inputAge > 0 && inputAge < 200 ) {
    person.age = inputAge;
}
```


모든 곳에서 이 검사를 사용하는 것은 불필요하고 지루합니다.

검사를 반복하지 않으려면 setter와 getter를 사용할 수 있습니다. getter 및 setter를 사용하면 클래스 속성에 대한 액세스를 제어할 수 있습니다.

각 속성에 대해:

* getter 메서드는 속성 값의 값을 반환합니다. getter는 accessor라고도 합니다.
* setter 메서드는 속성 값을 업데이트합니다. setter는 mutator라고도 합니다.




getter 메소드는 get 키워드로 시작하고 setter 메소드는 set 키워드로 시작합니다. 


```typescript
class Person {
    private _age: number;
    private _firstName: string;
    private _lastName: string;

 
    public get age() {
        return this._age;
    }

    public set age(theAge: number) {
        if (theAge <= 0 || theAge >= 200) {
            throw new Error('The age is invalid');
        }
        this._age = theAge;
    }

    public getFullName(): string {
        return `${this._firstName} ${this._lastName}`;
    }
}

```

이제 age다음과 같이 setter 메서드에 액세스할 수 있습니다
```typescript
let person = new Person();
person.age = 10;
```
setter에 대한 호출에는 일반 메서드처럼 괄호가 없습니다. 를 호출 person.age하면 agesetter 메서드가 호출됩니다. 잘못된 age값 을 할당하면 setter에서 오류가 발생합니다.


```typescript
person.age = 0;
```


오류:
```shell
Error: The age is invalid
```

당신이 액세스 할 때 person.age의 age게터가 호출됩니다.
```typescript
console.log(person.age);
```


다음은 firstName및 lastName속성에 getter 및 setter를 추가합니다 .

```typescript
class Person {
    private _age: number;
    private _firstName: string;
    private _lastName: string;

    public get age() {
        return this._age;
    }

    public set age(theAge: number) {
        if (theAge <= 0 || theAge >= 200) {
            throw new Error('The age is invalid');
        }
        this._age = theAge;
    }

    public get firstName() {
        return this._firstName;
    }

    public set firstName(theFirstName: string) {
        if (!theFirstName) {
            throw new Error('Invalid first name.');
        }
        this._firstName = theFirstName;
    }

    public get lastName() {
        return this._lastName;
    }

    public set lastName(theLastName: string) {
        if (!theLastName) {
            throw new Error('Invalid last name.');
        }
        this._lastName = theLastName;
    }

    public getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
}
```



## Inheritance 

클래스는 다른 클래스의 속성과 메소드를 다시 사용할 수 있습니다. 이것을 TypeScript에서는 상속이라고 합니다.

속성과 메서드를 상속하는 클래스를 자식 클래스 라고 합니다 . 그리고 속성과 메서드가 상속되는 클래스를 부모 클래스라고 합니다. 이 이름은 아이들이 부모로부터 유전자를 물려받는 특성에서 비롯됩니다.


상속을 사용하면 다시 작성하지 않고도 기존 클래스의 기능을 재사용할 수 있습니다.




다음 Person클래스 가 있다고 가정합니다 .
```typescript
class Person {
    constructor(private firstName: string, private lastName: string) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
    getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
    describe(): string {
        return `This is ${this.firstName} ${this.lastName}.`;
    }
}
```
클래스를 상속하려면 extends키워드 를 사용합니다 . 예를 들어 다음 Employee 클래스는 Person 클래스를 상속합니다.


```typescript
class Employee extends Person {
    //..
}
```
이 예에서 Employee는 자식 클래스이고 Person는 부모 클래스입니다.


### 생성자(Constructor) 


자식 클래스의 생성자에서 부모 클래스의 생성자를 호출하려면 super()구문 을 사용 합니다

```typescript
class Employee extends Person {
    constructor(
        firstName: string,
        lastName: string,
        private jobTitle: string) {
        
        // call the constructor of the Person class:
        super(firstName, lastName);
    }
}
```
다음은 Employee클래스 의 인스턴스를 생성합니다 .
```typescript
let employee = new Employee('John','Doe','Front-end Developer');
```

Employee 클래스는 Person 클래스의 메소드와 속성들을 상속받기 때문에 getFullName()과 describe() 메소드에 접근할 수 있습니다. 

```typescript
let employee = new Employee('John', 'Doe', 'Web Developer');

console.log(employee.getFullName());
console.log(employee.describe());

```


### Method overriding


Employee클래스에 자체 버전의 describe()메서드 가 있기 를 원하면 다음 Employee과 같이 클래스 에서 정의할 수 있습니다 .

```typescript
class Employee extends Person {
    constructor(
        firstName: string,
        lastName: string,
        private jobTitle: string) {

        super(firstName, lastName);
    }

    describe(): string {
        return super.describe() + `I'm a ${this.jobTitle}.`;
    }
}
```

super.methodInParentClass()를 사용하여 부모 클래스의 메소드를 호출한다. 


당신이 employee 개체의 describe() 메소드를 호출하면 ,  Employee클래스의 describe() 메소드가 실행된다. 


```typescript
let employee = new Employee('John', 'Doe', 'Web Developer');
console.log(employee.describe());
```


## Static Methods and Properties


### 정적 속성 
스턴스 속성과 달리 정적 속성은 클래스의 모든 인스턴스에서 공유됩니다.

정적 속성을 선언하려면 static키워드 를 사용합니다 . 정적 속성에 액세스하려면 className.propertyName구문 을 사용 합니다.


```typescript
class Employee {
    static headcount: number = 0;

    constructor(
        private firstName: string,
        private lastName: string,
        private jobTitle: string) {

        Employee.headcount++;
    }
}
```
이 예에서 는 headcount는 0으로 초기화된 정적 속성입니다. 새 개체가 생성될 때마다 값이 1씩 증가합니다.

다음은 두 개의 Employee객체를 생성 하고 headcount속성 값을 보여줍니다 . 예상대로 두 개를 반환합니다.

```typescript
let john = new Employee('John', 'Doe', 'Front-end Developer');
let jane = new Employee('Jane', 'Doe', 'Back-end Developer');

console.log(Employee.headcount); // 2

```



### 정적 메서드
정적 속성과 유사하게 정적 메서드도 클래스의 인스턴스 간에 공유됩니다. 정적 메서드를 선언하려면 static메서드 이름 앞에 키워드 를 사용합니다 .


```typescript
class Employee {
    private static headcount: number = 0;

    constructor(
        private firstName: string,
        private lastName: string,
        private jobTitle: string) {

        Employee.headcount++;
    }

    public static getHeadcount() {
        return Employee.headcount;
    }
}
```

정적 메서드를 호출하려면 className.staticMethod()구문 을 사용 합니다. 


```typescript
let john = new Employee('John', 'Doe', 'Front-end Developer');
let jane = new Employee('Jane', 'Doe', 'Back-end Developer');

console.log(Employee.getHeadcount); // 2
```



## Abstract Classes

추상 클래스는 일반적으로 확장할 파생 클래스의 공통 동작을 정의하는 데 사용됩니다. 일반 클래스 와 달리 추상 클래스는 직접 인스턴스화할 수 없습니다.

추상 클래스를 선언하려면 다음 abstract키워드 를 사용합니다 .


```typescript
abstract class Employee {
    //...
}
```

일반적으로 추상 클래스에는 하나 이상의 추상 메서드가 포함됩니다.

추상 메서드에는 구현이 포함되어 있지 않습니다. 메서드 본문을 포함하지 않고 메서드의 서명만 정의합니다. 파생 클래스에서 추상 메서드를 구현해야 합니다.

다음은 추상 메서드 Employee가 있는 getSalary()추상 클래스를 보여줍니다 .


```typescript
abstract class Employee {
    constructor(private firstName: string, private lastName: string) {
    }
    abstract getSalary(): number
    get fullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
    compensationStatement(): string {
        return `${this.fullName} makes ${this.getSalary()} a month.`;
    }
}
```


Employee클래스는 추상적 이기 때문에 새로운 객체를 생성할 수 없습니다. 다음 명령문은 오류를 발생시킵니다.

```typescript
let employee = new Employee('John','Doe');
```
오류:
```shell
error TS2511: Cannot create an instance of an abstract class.
```

다음 FullTimeEmployee 클래스는 Employee 클래스에서 상속합니다.

```typescript
class FullTimeEmployee extends Employee {
    constructor(firstName: string, lastName: string, private salary: number) {
        super(firstName, lastName);
    }
    getSalary(): number {
        return this.salary;
    }
}
```

이 FullTimeEmployee클래스에서 급여는 생성자에서 설정됩니다. 클래스 getSalary()의 추상 메서드 이기 때문에 클래스는 이 메서드를 구현해야 합니다. 이 예에서는 계산 없이 급여만 반환합니다.


**요약**
* 추상 클래스는 인스턴스화할 수 없습니다.
* Abstract 클래스에는 최소한 하나의 추상 메서드가 있습니다.
* 추상 클래스를 사용하려면 이를 상속하고 추상 메서드에 대한 구현을 제공해야 합니다.