# Event

웹 앱을 만들 때 이벤트에 대한 지식은 필수이다.

## 이벤트 핸들러와 이벤트 리스너

이벤트 핸들러 작성 예

```javascript
window.onload = function() {}
```

이벤트 리스너 작성 예

```javascript
window.addEventListener('load', function() {
})
```

**콜백함수** 이벤트가 발생했을 때 실행하는 함수를 콜백함수라고 한다.

> 이벤트 핸들러와 이벤트 리스너의 차이는 무엇인가? 바로 정의할 수 있는 숫자의 차이이다.

다음 코드에서 최초에 정의한 함수는 무효가 된다.

```javascript
window.onload = function() {
  alert("첫번째 함수")
}

window.onload = function() {
  alert("두번째 함수")
}
```

반면 이벤트 리스너는 몇 개든지 정의할 수 있다.

```javascript
    window.addEventListener('load', function() {
      alert("첫번째 리스너")
    }, false)
    window.addEventListener('load', function() {
      alert("두번째 리스너")
    }, false)
```

## load 이벤트

지자바스크립트를 실행하면서 페이지 로딩이 완료되는 것을 기다리려고 load 이벤트에 대한 이벤트 리스너를 등록했다. 하지만 load 이벤트는 페이지에 포함된 많은 리소스들을 모두 읽어 들이지 않는한 발생하지 않는다.

페이지에 포함된 외부 리소스가 적다면 상관 없지만, 수많은 외부 리소스를 로드하는 페이지라면 load 이벤트의 발생은 체감할 수 있을 만큼 느려진다.

## DOMContentLoaded 이벤트

페이지에서는 대부분 DOM 트리에만 접근하면 되고 HTML 파일 이외의 외부리소가 필요하지 않다. 이렇게 빠르게 스크립트를 실행하려면 DOMContentLoaded 이벤트를 사용한다. 이 이벤트는 HTML을 로드하고 스크립트를 로드한 후, 브라우저 내부에서 DOM이 구성된 시점에서 발생한다.

* DOMContentLoaded 이벤트와 짝을 이루는 이벤트 핸들러는 없다. 따라서 DOMContentLoaded 이벤트는 이벤트 리스너에서 처리해야 한다.
* DOMContentLoaded 이벤트는 스타일 시트로 문서를 꾸미기 전에 발행한다. 그래서 자바스크립트로 요소의 좌표 정보를 다루면 문제가 발생한다.

```javascript
    window.addEventListener('DOMContentLoaded', function() {
      alert("DOMContentLoaded Event")
    }, false)
```
