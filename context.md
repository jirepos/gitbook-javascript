# context

## 컨텍스트(Context)

자바스크립트를 작성할 때 코드를 효율적으로 작성하기 위해서 보통은 함수나 객체를 생성하여 코드를 작성한다. 또는 전역에 코드를 작성하기도 한다. 전역은 기본적인 영역으로 함수나 객체 안의 영역이 아닌 곳을 의미한다. 이렇게 자바스크립트 코드는 어떤 영역 안에서 실행이되는 이 실행되는 영역을 컨텍스트(Context)라고 부른다. 더 정확히는 실행컨텍스트(Excecution Context)라고 한다.

### 전역 컨텍스트(Global Context)

일단 처음 코드를 실행(여기서 실행은 브라우저가 스크립트를 로딩해서 실행하는 걸 말합니다)하는 순간 모든 것을 포함하는 전역 컨텍스트가 생깁니다. 모든 것을 관리하는 환경입니다. 페이지가 종료될 때까지 유지됩니다.

```html
<script>
// 여기가 전역 컨텍스트 
let a = "hello"  // 전역 컨텍스트에 있는 변수 
console.log(a)    // 전역 컨텍스트에 있는 코드
</script>
```

\<script> 태그 내에 있는 코드는 전역 컨텍스트에 있고, 전역컨텍스트에서 실행된다.

### 함수 컨텍스트(Function Context)

다읔과 같이 전역 실행 컨텍스트 안에 있는 코드 print()는 위에 선언된 print() 함수를 호출한다.

```javascript
function print() {
  let msg = "hello" 
  console.log(msg)
}

print() // print 함수 호출 
```

전역 실행 컨텍스트에서 함수를 호출하면 새로운 Function execution context를 생성하고 이를 execution statck에 쌓는다. print() 함수 안의 코드들은 함수 실행 컨텍스트에서 실행된다.

#### Scope

스코프는 변수와 매개변수의 접근성과 생존기간을 의미한다. 다음의 코드를 살펴보자.

```html
<script>
  var global_scope = "global scope"
  function parent(parent_param) {
    var local_scope_a = "a" 

    function child() {
      var local_scope_b = "b"
    }
  }
</script>
```

전역 컨텍스트에 선언된 global\_scope 변수는 전역 스코프에 선언되어 있다. local\_scope\_a 변수는 parent 함수 스코프에 선언되어 있다. 마지막으로 local\_Scope\_b 변수는 child 함수 스코프에 선언되어 있다.

child 함수 내부에 선언된 local\_scope\_b는 child 함수 내부에서만 접근할 수 있다. local\_scope\_a 변수는 parent 함수 내부에서 접근할 수 있고 child 함수내에서 접근할 수 있다. global\_scope 변수는 전역에서 뿐만 아니라 parent 함수와 child 함수에서도 접근할 수 있다.

함수 내부에 선언된 변수는 함수가 실행 중에만 유효하다.

```html
<script>
  var global_scope = "global scope"
  function parent(parent_param) {
    var local_scope_a = "a"  
    global_scope =" 다른 값"  // 전역 스코프의 변수는 함수에서 접근 가능 

    function child() {
      var local_scope_b = "b"
      global_scope =" 또 다른 값"  // 전역 스코프의 변수는 함수에서 접근 가능 
      local_scope_a = "aa" // 상위 함수의 변수는 내부의 함수에서 접근 가능
    }
  }
</script>
```

#### Scope 체인

위의 코드에서 child 함수에서 사용한 변수 global\_Scope는 child 함수 내에 선언되어 있지 않다. 그러면 자바스크립트는 parent에서 그 변수를 찾는다. 없으면 다시 글로벌 스코르까지 올라가서 변수 global\_scope를 찾는다. 이것을 스코프 체인(scope chain)이라고 한다.

### Hoisting

호이스팅(Hoisting)의 개념 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것을 말한다.

* var 변수 선언과 함수선언문에서만 호이스팅이 일어난다.
* var 변수/함수의 선언만 위로 끌어 올려지며, 할당은 끌어 올려지지 않는다.
* let/const 변수 선언과 함수표현식에서는 호이스팅이 발생하지 않는다.

다음 코드를 보면 함수 선언은 뒤에 나오고 선언이 있기 전에 함수를 호출하고 있다.

```javascript

foo()  // 함수의 선언이 뒤에 나오고 선언되기 이전에 사용 가능 
bar()

function foo() {
  console.log('foo')
}
function bar() {
  console.log('bar')
}
```

자바스크립트는 실행 전에 아래에 선언된 함수들을 모두 위로 올린다. 즉, 다음과 같이 변경된다.

```javascript

function foo() {
  console.log('foo')
}
function bar() {
  console.log('bar')
}

foo()  // 함수의 선언이 뒤에 나오고 선언되기 이전에 사용 가능 
bar()
```

**주의할 점**

* 코드의 가독성과 유지보수를 위해 호이스팅이 일어나지 않도록 한다. 호이스팅을 제대로 모르더라도 함수와 변수를 가급적 코드 상단부에서 선언하면, 호이스팅으로 인한 스코프 꼬임 현상은 방지할 수 있다.
* let/const를 사용한다. var를 쓰면 혼란스럽고 쓸모없는 코드가 생길 수 있다. 그럼 왜 var와 호이스팅을 이해해야 할까?

## this의 이해

대부분의 경우 this의 값은 함수를 호출한 방법에 의해 결정됩니다. 실행중에는 할당으로 설정할 수 없고 함수를 호출할 때 마다 다를 수 있습니다. ES5는 함수를 어떻게 호출했는지 상관하지 않고 this 값을 설정할 수 있는 bind 메서드를 도입했고, ES2015는 스스로의 this 바인딩을 제공하지 않는 화살표 함수를 추가했습니다(이는 렉시컬 컨텍스트안의 this값을 유지합니다).
