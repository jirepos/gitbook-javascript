# JavaScript에서 this

면 **실행 컨텍스트는 실행 가능한 코드가 실행되기 위해 필요한 환경** 이라고 말할 수 있겠다. 여기서 말하는 실행 가능한 코드는 아래와 같다.

* 전역 코드 : 전역 영역에 존재하는 코드
* Eval 코드 : [eval 함수](https://poiemaweb.com/js-built-in-object#2121-eval)로 실행되는 코드
* 함수 코드 : 함수 내에 존재하는 코드

## 컨텍스트(Context)

자바스크립트에서는 자바스크립트 코드가 실행되는 위치를 의미하는데&#x20;







## 전역 컨텍스트(Global Context)



일단 처음 코드를 실행(여기서 실행은 브라우저가 스크립트를 로딩해서 실행하는 걸 말합니다)하는 순간 모든 것을 포함하는 **전역 컨텍스트**가 생깁니다. 모든 것을 관리하는 환경입니다. 페이지가 종료될 때까지 유지됩니다.

```
<script>
// 여기가 전역 컨텍스트 
let a = "hello"  // 전역 컨텍스트에 있는 변수 
console.log(a)    // 전역 컨텍스트에 있는 코드
</script>
```

\<script> 태그 내에 있는 코드는 전역 컨텍스트에 있고, 전역컨텍스트에서 실행된다. &#x20;

### 실행 컨텍스트(Execution Context)

실행컨텍스트라는 말을 사용하는데 위의 코드는 전역컨텍스트에서 실행되고 있기 때문에 위의 코드의 실행 컨텍스트(Execution Context)는 전역 컨텍스트이다.



대부분의 경우 `this`의 값은 함수를 호출한 방법에 의해 결정됩니다. 실행중에는 할당으로 설정할 수 없고 함수를 호출할 때 마다 다를 수 있습니다. ES5는 [`함수를 어떻게 호출했는지 상관하지 않고 this 값을 설정할 수 있는`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this) [`bind`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global\_Objects/Function/bind) 메서드를 도입했고, ES2015는 스스로의 `this` 바인딩을 제공하지 않는 [화살표 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow\_functions)를 추가했습니다(이는 렉시컬 컨텍스트안의 `this`값을 유지합니다).



















함수 컨텍스트&#x20;











다음과 같이 this의 값을 출력해 보자.&#x20;

```
<script>
console.log(this)
</script>
```

다음과 같이 window가 출력된다.&#x20;

![](<../.gitbook/assets/image (3).png>)

함수나 코드 블럭 안이 아니라 최상위에 선언이 되는 장소가 전역 컨텍스트이다.  전역 컨텍스트는 window 객체이다.&#x20;



> this는 어떻게 정의되었는지가 아니라 어떻게 호출되었느냐에 따라 결정된다.

```
      let obj = {
        message: "hello",
        print() {
          console.log(this.message);  // this는 obj를 가리킨다. 
        }
      };

      obj.print();
```

print() 메소드 안의 this는 obj를 가리킨다.&#x20;









