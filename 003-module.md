# Module

## Syntax
```jsx
import defaultExport from "module-name";
import * as name from "module-name";
import { export1 } from "module-name";
import { export1 as alias1 } from "module-name";
import { export1 , export2 } from "module-name";
import { export1 , export2 as alias2 , [...] } from "module-name";
import defaultExport, { export1 [ , [...] ] } from "module-name";
import defaultExport, * as name from "module-name";
import "module-name";
var promise = import("module-name");
```


## 프로젝트 구조

```
📂project_root
  📂js
    📄index.js
    📄lib.js
  📄index.html
```

## index.html

type="module"을 설정하여 index.js를 로드한다.

```markup
<head>
  <script src="/js/index.js" type="module"></script>
</head>
```

## 기본 내보내기

내보내기(export)는 **유명(named) 내보내기와 기본(default) 내보내기**가 있다. 유명 내보내기는 여러개 존재할 수 있지만 기본 내보내기는 하나만 가능하다.

### 변수

lib.js에 name 변수를 정의한다.

```javascript
// lib.js
// 기본 내보내기 
export default {  
  name: "Latte"
}
```


**default로 export한 것은 임으로 이름을 정의할 수 있다**. lib.name과 같이 사용한다.

```javascript
// index.js
// default는 이름을 마음대로 정할 수 있다. 
import lib from './lib.js'
console.log(lib.name)
```

### 함수

이름 없는 함수를 하나 정의하고 export한다.

```javascript
// lib.js

export default () =>  {
  console.log("hello")
}
```

임의의 이름으로 import할 수 있다. 아래는 hello라는 이름으로 import 했다. hello는 함수이므로 실행할 수 있다

```javascript
// index.js
import hello from './lib.js'
hello()
```

### 객체

익명 객체를 만들고 export 한다.

```javascript
// lib.js
export default  {
  name: "Latte", 
  getName() {
    return this.name; 
  }
}
```

obj라는 임의의 이름으로 import를 한다. obj.name과 같이 객체의 속성을 사용할 수 있고 obj.getName()과 같이 함수를 사용할 수 있다.

```javascript
// index.js
import obj from './lib.js'
console.log(obj.name) 
console.log(obj.getName())
```

## 유명 내보내기

유명 내보내기는 여러 값을 내보낼 때 사용한다. lib.js에 변수, 함수, 객체를 정의하고 내보낸다.

```javascript
// lib.js
let moduleName = "common"
let add = (a,b) => { 
  return a + b
}
let calc = {
  multiply(a,b,) {
    return a * b
  }
}
export { moduleName, add, calc}
```

index.js에서 lib.js에서 내보낸 이름으로 import한다.

```javascript
// index.js
import { moduleName, add, calc } from './lib.js'

console.log(moduleName)
console.log(add(1,2))
console.log(calc.multiply(2,2))
```

## 내보내기 혼용

lib.js에서 moduleName을 default로 내보내고 나머지는 유명 내보내기를 사용한다.

```javascript
// lib.js
let moduleName = "common"
let add = (a,b) => { 
  return a + b
}
let calc = {
  multiply(a,b,) {
    return a * b
  }
}
// moduleName은 default로 내보내고 
export { moduleName as default , add, calc}
```

import할 때에 default는 'as 별칭'을 사용하여 import 한다.

```javascript
// index.js

import { default as moduleName, add, calc } from './lib.js'

console.log(moduleName)
console.log(add(1,2))
console.log(calc.multiply(2,2))
```

아래와 같이 import를 하면 default로 내보내기한 moduleName만 import하게 된다.

```javascript
// index.js
import newName from './lib.js'

console.log(newName)
```

기본 내보내기와 유명 내보내기를 아래와 같이 import할 수도 있다. 콤마와 { }를 사용하여 유명 내보내기로 내보낸 것들을 { } 안에 나열한다.

```javascript
// index.js
import newName, { add } from './lib.js'

console.log(newName)
console.log(add(1,2)
```


## 바인딩 없이 모듈만 실행하기
단순히 특정 모듈을 불러와 실행만 할 목적이라면, import만 사용하는 것이 좋다. 어떠한 바인딩 없이 모듈 전체의 사이드 이펙트만 가져온다. 

```jsx
import "mymodule.js";
```


mymodule.js에 다음과 같이 정의되어 있다고 가정한다. 
```jsx
funtion hello() { 
  console.log();
}

console.log("start"); 
```

이 모듈을 다음과 같이 모듈을 import 하면 
```jsx
import "mymodule.js";
```
모듈의 console.log("start")는 실행하지만, hello() 함수는 가져오지 않는다. 즉, 모듈의 전역 코드를 실행하지만 아무것도 가져오지 않는다. 

> Import an entire module for side effects only, without importing anything. This runs the module's global code, but doesn't actually import any values.



다음은 이름이 없다고 에러가 출력된다. 
```jsx
import "mymodule.js"; 

hello();  // 가져오지 않기 때문에 오류가 발생한다. 

```
이것은 동적 가져 오기 에서도 작동 한다. 

```jsx
(async () => {
  if (somethingIsTrue) {
    // 부작용을위한 모듈 가져 오기
    await import('/modules/my-module.js');
  }
})();
```


## 동적 가져오기 



```jsx
  import('/modules/my-module.js')
      .then(module => {
        module.loadPageInto(main);
      })
      .catch(err => {
        main.textContent = err.message;
      });
```
















