# Event

이벤트를 사용하는 방법을 더 자세히 알아본다.

## 이벤트 등록

object.addEventListener를 사용하여 등록한다.

```
object.addEventlistener(이벤트명, 콜백함수, [캡쳐링여부])
```

### 버블링과 캡쳐링

**버블링**\
다음과 같이 중첩된 요소가 있는 마크업에서 em을 클릭하면 div에 할당된 이벤트 리스너가 동작한다.

```html
<div>
  <em>여기를 클릭한다</em>
</div>
```

한 요소에 이벤트가 발생하면 이 요소에 할당된 핸들러가 동작하고 이어서 부모 요소의 핸들러가 동작한다. 가장 최상단의 조상 요소를 만날 때까지 이 고장이 반복되면서 각각에 할당된 핸들러가 동작한다.

**버블링 중단하기**\
이벤트 버블링은 타깃 이벤트에서 시작해서 요소를 거쳐 document 객체를 만날 때까지 각 노드에서 모두 발생한다. 몇몇 이벤트는 window 객체까지 거슬러 올라가기도 한다. 이 때도 모든 핸들러가 호출된다.

그런데 핸들러에게 이벤트를 완전히 처리하고 난 후 버블링을 중단하도록 명령할 수도 있다.

이벤트 객체의 메서드인 event.stopPropagation()를 사용하면 된다. 아래 예시에서 \<button>을 클릭해도 body.onclick은 동작하지 않는다.

```html
<body onclick="alert(`버블링은 여기까지 도달하지 못합니다.`)">
  <button onclick="event.stopPropagation()">클릭해 주세요.</button>
</body>
```

**캡처링**

이벤트엔 버블링 이외에도 ‘캡처링(capturing)’ 이라는 흐름이 존재한다. 실제 코드에서 자주 쓰이진 않지만, 종종 유용한 경우가 있으므로 알아보자.

표준 DOM 이벤트에서 정의한 이벤트 흐름엔 3가지 단계가 있다.

1. 캡처링 단계 – 이벤트가 하위 요소로 전파되는 단계
2. 타깃 단계 – 이벤트가 실제 타깃 요소에 전달되는 단계
3. 버블링 단계 – 이벤트가 상위 요소로 전파되는 단계

> 캡처링 단계를 이용해야 하는 경우는 흔치 않기 때문에, 이전까진 주로 버블링만 설명했다. 캡처링에 관한 코드를 발견하는 일은 거의 없을 것이다.

## 이벤트 제거

object.removeEventListener를 사용하여 제거한다.

```
object.removeEventListener(이벤트명, 콜백함수)
```

## event.target

부모 요소의 핸들러는 이벤트가 정확히 어디서 발생했는지 등에 대한 자세한 정보를 얻을 수 있다. 이벤트가 발생한 가장 안쪽의 요소는 타깃(target) 요소라고 불리고, event.target을 사용해 접근할 수 있다.

## Key Event

자바스크립트에서 샤용할 수 있는 주요 이벤트들은 다음과 같다.

* **KeyBoard Event**
  * **keydown** 키를 눌렀을 때 발생
  * **keyup** 키에서 손을 땟을 때 발생
* Mouse Event
  * **mousedown** 마우스를 클릭 했을 때 발생
  * **mouseout** 마우스가 특정 객체 밖으로 나갔을 때 발생
  * **mouseover** 마우스가 특정 객체 위로 올려졌을 때 발생
  * **mousemove** 마우스가 움직였을 때 발생
  * **mouseup** 마우스에서 손을 땟을 때 발생
* **click** 클릭시 발생
* **focus** 포커스를 얻었을 때 발생
* **select** select 이벤트는 어떤 텍스트가 선택되었을 때 발생
* **change** 변동이 있을 때 발생

## Keyboard event

### keydown event

사용자가 키보드의 키를 눌렀을 때 발생한다.

```javascript
      var input1 = document.getElementById('input1')
      input1.addEventListener('keydown', function(event) {
        console.log(event)
        console.log(event.code)
        console.log(event.keyCode)
      })
```

### keyup event

사용자가 키보드의 키를 눌렀다가 떼었을 때 발생한다.

```javascript
      input1.addEventListener('keyup', function(event) {
        console.log(event)
        console.log(event.code)
        console.log(event.key)
        console.log(event.keyCode)
      })
```

### keypress event

사용자가 키보드를 눌렀을 때 발생한다.

* 사용자가 키보드를 눌렀을 때 발생한다.
* Alt, Ctrl, Shift, Esc 키등 몇 가지 키에서는 이 이벤트를 발생시키지 않는다.
* 이 이벤트는 사용을 권장하지 않는다.

## Mouse Event

마우스와 관련된 이벤트들을 살펴 본다.

1. **onmouseover**: 해당 객체의 영역위에 커서가 진입하는 순간 발생
2. **onmouseout**: 해당 영역에서 커서가 빠져나가는 순간 발생
3. **onmousedown**: 해당 객체의 영역에서 마우스 버튼이 눌려지는 순간 발생
4. **onmouseup**: 해당 객체의 영역에서 마우스 버튼이 떼는 순간 발생
5. **onmousemove**: 해당 객체의 영여겡서 커서가 움직이는 순간 발생

## mouseover event

해당 객체의 영역위에 커서가 진입하는 순간 발생한다.

```javascript
      var div1 = document.getElementById('div1')
      div1.addEventListener('mouseover', function(event) {
        console.log(event) 
        console.log(event.x)
        console.log(event.y)
      })
```

## mousemove event

해당 객체의 영여겡서 커서가 움직이는 순간 발생한다.

```javascript
      div1.addEventListener('mousemove', function(event) {
        //console.log(event) 
        console.log(event.x)
        console.log(event.y)
      })
```

## Click Event

요소를 클릭할 때 발생한다.

```javascript
      var span1 = document.getElementById("span1")
      span1.addEventListener('click', function(event) {
        console.log(event)
        console.log(event.target)
      })
```

## Focus Event

요소가 포커스를 받았을 때 발생한다.

```javascript
      input1.addEventListener('focus', function(event) {
        console.log(event)
      })
```

## Select Event

select 이벤트는 어떤 텍스트가 선택되었을 때 발생된다.

```javascript
      var input2 = document.getElementById("input2")
      input2.addEventListener('select', function(event) {
        console.log(event)
      })
```

## Change Event

input, select ,textarea 요소의 값이 변경되면 발생한다.

```javascript
      var icecream = document.getElementById("ice-cream")
      icecream.addEventListener('change', function(event) {
        console.log(event)
        console.log(event.target.value)
        console.log(event.target.selectedIndex)
        console.log(event.target.options[event.target.selectedIndex].text)
      })
```
