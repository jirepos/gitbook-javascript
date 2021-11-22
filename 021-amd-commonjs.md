# AMD와 CcommonJS


## 모듈화의 세가지 방식
* CommonJS
  * Node.js 가 사용
* AMD
  * Require.js가 사용 
* ES2015
  * 브라우저 표준 


### AMD의 모듈 명세 
AMD만의 특징으로  define() 함수가 있다.
* 이 함수로 파일 스코프의 역할을 대신한다. 
* 즉, 일종의 네임스페이스 역할을 하여 모듈에서 사용하는 변수와 전역변수를 분리한다. 
* 물론 define() 함수는 전역함수로 AMD 명세를 구현하는 서드파티 벤더가 모듈 로더에 구현해야 한다.


```jsx
define(id?, dependencies?, factory);  
```
**id**
* 모듈을 식별하는데 사용하는 인수, 선택적이다. 

**dependencies**
* 의존성을 나타내는 배열 
* 반드시 먼저 로드돼야 하는 모듈을 나타낸다. 
* 먼저 로드된 모듈은 세번째 인수인 팩토리 함수의 인자로 넘겨진다. 
* 두 번째 인수 역시 선택적으로 사용하지만, 생략한다면 ['require', 'exports', 'module']이라는 이름이 기본으로 지정된다


다음은 
* alpha라는 모듈을 정읳ㄴ다. 
* beta 모듈이 필요하다. 


```jsx
define("alpha", ["require", "exports", "beta"], function (require, exports, beta) {  

  exports.verb = function() {

  // 넘겨받는 인수를 사용해도 되고
 return beta.verb();

  // 또는 require()를 이용해
  // 얻어 온 모듈을 사용해도 된다.
  return require("beta").verb();  
 }
});
```

다음 예제는 첫번째 인수를 생략하였고 alpha라는 모듈을 필요로 한다.  
* rquire() 함수로 이 모듈을 사용하고 싶다면 , 이 모듈이 정의된 파일의 경로를 지정해야 한다. 


```jsx
define(["alpha"], function (alpha) {  
    return {  
      verb: function(){  
      return alpha.verb() + 2;  
    }
  };
});

// 위 모듈이  http://somewhere.com/js/modelBeta.js 로 접근이 가능하다고 가정하면,

require(["/js/modelBeta.js"], function(moduelBeta)(){  
  // moduleBeta를 활용하는 실제 코드는 여기에..

});
```

다음은 의존성 없는 모듈을 정의한다.  첫 번째 id 식별자가 없으므로, 모듈이 정의된 파일의 경로가 자종으로 식별자로 지정된다. 
```jsx
define({  
  add: function(x, y){  
    return x + y;  
  }
});
```



### CommonJS의 모듈 명세 
자바스크립트의 모듈화 명세를 만든 대표적인 그룹 중 'CommonJS'가 있고, 이 CommonJS의 명세가 현재 node의 표준이 되어있다.


아래 두 가지 규칙이 있지만, 특별한 상황이 아니면 module.exports를 사용하는 것이 권장된다. 

* 여러 개의 객체를 내보낼 경우, exports 변수의 속성으로 할당한다.
* 딱 하나의 객체를 내보낼 경우, module.exports 변수 자체에 할당한다.

**내보내기**
```jsx
// func.js
const function func1() {

}

module.exports = func1
```


**불러오기**
```jsx
// use.js
const func1 = require("./func");
```



### UMD(Universal Module Definition) 
CommonJS와 AMD를 통합하기 위한 하나의 패턴으로 다음과 같이 작성한다. 
```jsx
var datetimepickerFactory =  function ($) {

}

;(function (factory) {
	if ( typeof define === 'function' && define.amd ) {
		// AMD. Register as an anonymous module.
		define(['jquery', 'jquery-mousewheel'], factory);
	} else if (typeof exports === 'object') {
		// Node/CommonJS style for Browserify
		module.exports = factory(require('jquery'));;
	} else {
		// Browser globals
		factory(jQuery);
	}
}(datetimepickerFactory));
```


