# JavaScript Function

함수는 JavaScript에서 기본적인 구성 블록 중의 하나이다. 함수는 작업을 수행하거나 값을 계산하는 문장 집합 같은 자바스크립트 절차이다.

## 함수 선언

함수 정의(또는 함수 선언)은 다음과 같은 함수 키워드로 구성된다.

* 함수의 이름
* 괄호 안에서 쉼표로 분리된 함수의 매개변수 목록
* 중괄호 { } 안에서 함수를 정의하는 자바스크립트 표현

```javascript
function square(number) {
  return number * number ;
}
```

return 문은 함수에 의해 반환된 값을 지정한다.

return 문이 없을 수도 있다.

```javascript
function funcA() {
  console.log('funcA')
}
```

### 함수 표현식

함수 표현식( function expression)에 의해서 함수가 만들어 질 수도 있다. 이 같은 함수를 익명이라고 한다. 이 말은 모든 함수가 이름을 가질 필요는 없다는 것을 뜻한다.

```javascript
    var funcD = function() { 
      console.log('funcD')
    }
```

### 함수의 범위

함수 내에서 정의된 변수는 변수가 함수의 범위에서만 정의되어 있기 때문에, 함수 외부의 어느 곳에서든 액세스할 수 없다. 그러나, 함수가 정의된 범위 내에서 정의된 모든 변수나 함수는 액세스할 수 있다. 즉, 전역함수는 모든 전역 변수를 액세스할 수 있다. 다른 함수 내에서 정의 된 함수는 부모 함수와 부모 함수가 액세스 할 수 있는 다른 변수에 정의된 모든 변수를 액세스할 수 있다.

```javascript
// The following variables are defined in the global scope
var num1 = 20,
    num2 = 3,
    name = "Chamahk";

// This function is defined in the global scope
function multiply() {
  return num1 * num2;
}

multiply(); // Returns 60

// A nested function example
function getScore () {
  var num1 = 2,
      num2 = 3;

  function add() {
    return name + " scored " + (num1 + num2);
  }

  return add();
}

getScore(); // Returns "Chamahk scored 5"
```

## 클로저

클로저는 자바스크립트의 강력한 기능 중 하나입니다. 자바스크립트는 함수의 중첩(함수 안에 함수를 정의하는것)을 허용하고, 내부함수가 외부 함수 안에서 정의된 모든 변수와 함수들을 완전하게 접근 할 수 있도록 승인해준다.(그리고 외부함수가 접근할수 있는 모든 다른 변수와 함수들까지) 그러나 외부 함수는 내부 함수 안에서 정의된 변수와 함수들에 접근 할 수 없다.

```javascript
var pet = function(name) {   // 외부 함수는 'name'이라 불리는 변수를 정의합니다.
  var getName = function() {
    return name;             // 내부 함수는 외부 함수의 'name' 변수에 접근합니다.
  }
  return getName;            // 내부 함수를 리턴함으로써, 외부 범위에 노출됩니다.
},
myPet = pet("Vivie");

myPet();                     // "Vivie"로 리턴합니다.
```

## 함수 정의의 다양한 형태

global 영역에 정의된 함수는 다양한 방법으로 정의될 수 있다.

```javascript
   function funcA() {
      console.log('funcA')
    }
    window.funcB = function() {
      console.log('funcB')
    }
    window['funcC'] = function() {
      console.log('funcC')
    }
    var funcD = function() { 
      console.log('funcD')
    }

    var funcE = () => {
      console.log('funcE')
    }
    // parameter가 있는 함수 
    function funcF(name) {
      console.log(name)
    }
    function funcG(name, age) {
      console.log(name + "/" + age)
    }

    // 일회용 객체에서의 함수 선언 
    var obj = { 
      funcA() {
        console.log('funcA')
      },
      funcB() {
        console.log('funcB')
      }
    }

    
    window.addEventListener("DOMContentLoaded", function () {
      funcA()
      funcB()
      funcC()
      window['funcD']()
      funcE()
      funcF('kim')
      funcG('kim', 12)
      obj.funcA()
      obj.funcB()

    })
```

## 화살표 함수

파라미터가 없는 함수를 다음과 같이 정의할 수 있다.

```javascript
    var funcE = () => {
      console.log('funcE')
    }
```

화살표 함수의 다양한 사용방법은 아래를 참고한다.

```javascript
// 매개변수가 없는 경우
var foo = () => console.log('bar');
foo(); // bar

// 매개변수가 하나인 경우
var foo = x => x;
foo('bar'); // bar

// 매개변수가 여려개인 경우
var foo = (a, b) => a + b; // 간단하게 한줄로 표현할 땐 "{}" 없이 값이 반환됩니다.
foo(1, 2); // 3

var foo = (a, b) => { return a + b }; 
foo(1, 2); // 3

var foo = (a, b) => { a + b }; // "{}"를 사용했는데 return이 없을 때 
foo(1, 2); // undefined

var foo = (a, b) => { // 여러줄 썼을 때
	var c = 3;
	return a + b + c;
}
foo(1, 2, 3) // 6
/*
"{}"를 사용하면 값을 반환할 때 return을 사용해야합니다.
"{}"를 사용하지 않으면 undefied를 반환합니다.
"{}"을 사용할 때는 여러줄을 썼을 때 사용합니다.
*/

// 객체를 반환할 때
var foo = () => ( { a: 1, b: 2, c: 3 } );
foo(); // { a: 1, b: 2, c: 3 };
```
