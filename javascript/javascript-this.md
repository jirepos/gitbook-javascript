# JavaScript에서 this

자바스크립트의 실행 환경에 대해서 살펴보자.&#x20;

## 컨텍스트(Context)

자바스크립트를 작성할 때 코드를  효율적으로 작성하기 위해서 보통은 함수나 객체를 생성하여 코드를 작성한다.  또는 전역에 코드를 작성하기도 한다. 전역은 기본적인 영역으로 함수나 객체 안의 영역이 아닌 곳을 의미한다.&#x20;

이렇게 자바스크립트 코드는 어떤 영역 안에서 실행이되는 이 실행되는 영역을 컨텍스트(Context)라고 부른다.  더 정확히는 실행컨텍스트(Excecution Context)라고 한다.&#x20;



### 전역 컨텍스트(Global Context)



일단 처음 코드를 실행(여기서 실행은 브라우저가 스크립트를 로딩해서 실행하는 걸 말합니다)하는 순간 모든 것을 포함하는 **전역 컨텍스트**가 생깁니다. 모든 것을 관리하는 환경입니다. 페이지가 종료될 때까지 유지됩니다.

```
<script>
// 여기가 전역 컨텍스트 
let a = "hello"  // 전역 컨텍스트에 있는 변수 
console.log(a)    // 전역 컨텍스트에 있는 코드
</script>
```

\<script> 태그 내에 있는 코드는 전역 컨텍스트에 있고, 전역컨텍스트에서 실행된다. &#x20;



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









