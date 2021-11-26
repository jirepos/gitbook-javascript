## CSS 선택자를 사용한 querySelectorAll

## 선택자
### 기본선택자
**태그 선택자**
```shell
E
```

**클래스 선택자** 
```
.className
```

**아이디 선택자**

```xml
#itsId
```

**하위 선택자 vs 자식 선택자**

```xml
E F // E요소의 자손인 F 
E>F // E요소의 자식인 F
```

자식 선택자는 부모의 바로 아래 자식 요소에만 적용
하위 선택자는는 부모 요소에 포함된 모든 하위 요소 

**인접 형재 선택자와 일반 형제 선택자**

```xml
E+F  // E 요소를 뒤따르는 F 요소 (E와 F 사이에 다른 요소가 존재하면 선택하지 않는다)
E~F  // E 요소가 앞에 존재하면 F 선택( E가 F보다 먼저 등장하지 않으면 선택하지 않는다)
```

### 속성 선택자
```shell
E[attr] attr 속성이 포함된 E 선택
E[attr="val"] attr 속성의 값이 정확하게 'val'과 일치하는 E 
E[attr~="val"] attr 속성의 값이 'val'을 포함하는 요소(공백으로 분리된 값이 일치해야)
E[attr^="val"] attr 속성의 값이 val로 시작 
E[attr$="val"] attr 속성의 값이 val로 끝나는 
E[attr*="val"] attr 속성의 값이 'val'이 포함되는 요소 
E[attr|="val"] attr 속성의 값이 'val'이거나 'val'로 시작하는 
```



### 가상 선택자 
```shell
E[attr] attr 속성이 포함된 E 선택
E[attr="val"] attr 속성의 값이 정확하게 'val'과 일치하는 E 
E[attr~="val"] attr 속성의 값이 'val'을 포함하는 요소(공백으로 분리된 값이 일치해야)
E[attr^="val"] attr 속성의 값이 val로 시작 
E[attr$="val"] attr 속성의 값이 val로 끝나는 
E[attr*="val"] attr 속성의 값이 'val'이 포함되는 요소 
E[attr|="val"] attr 속성의 값이 'val'이거나 'val'로 시작하는 
```

### 구조적 가상 선택자
```
E::root 문서의 최상위 요소 root
E::nth-child(n) 지정된 순서와 일치하는 요소가 E라면 선택
E::nth-last-child(n) 뒤로부터 지정된 순서와 일치하는 E 요소 선택
```

## querySelectorAll 활용 

요소를 선택하고 forEach()를 활용하여 요소에 속성을 변경하거나 하는 처리르 할 수 있다. 
```jsx
let li2 = d.querySelectorAll("div > div >  ul li")
li2.forEach( e => {
  e.style.backgroundColor = "blue"
  if(e.matches('li')) {
    console.log("li element")
  }
  if (elem.matches('a[href$="zip"]')) {
    alert("주어진 CSS 선택자와 일치하는 요소: " + elem.href );
  }
})
```    

### Element.closet()
기준 Element 에서부터 closest() 메소드를 통해 자신부터 부모 요소 단위로 출발하여 각 요소가 지정한 선택자에 만족할 때까지 탐색한다(문서 루트까지 이동). 이 중 가장 가깝게 조건에 만족한 부모 요소가 반환되며, 조건에 만족한 요소가 없으면 null 값을 반환한다.

```
var closestElement = targetElement.closest(selectors);
```

> Explorer에서는 지원하지 않는다. 

```html
<article>
  <div id="div-01">Here is div-01
    <div id="div-02">Here is div-02
      <div id="div-03">Here is div-03</div>
    </div>
  </div>
</article>

```

```jsx
var el = document.getElementById('div-03');

var r1 = el.closest("#div-02");
// id=div-02 조건이 만족하므로 속성을 가진 부모 요소가 반환된다.

var r2 = el.closest("div div");
// div 요소에 만족한 요소 중 div 자식을 가리키므로, id=div-03 자신이 만족된다.

var r3 = el.closest("article > div");
// 가장 가까운 article 요소 바로 하위의 div 요소 id=div-01 속성을 가진 요소가 반환된다.

var r4 = el.closest(":not(div)");
// div 요소가 아닌 가장 가까운 부모 article 요소가 반환된다.
```



### matches() 사용 
이 matches()메서드는 Element제공된 항목에 의해 선택 selectorString되는지 확인한다. 즉, 요소가 선택자인지 확인한다. 
```jsx
var result = element.matches(selectorString);
```

```html
<li>Orange-winged parrot</li>
  <li class="endangered">Philippine eagle</li>
  <li>Great white pelican</li>
</ul>

<script type="text/javascript">
  var birds = document.getElementsByTagName('li');

  for (var i = 0; i < birds.length; i++) {
    if (birds[i].matches('.endangered')) {
      console.log('The ' + birds[i].textContent + ' is endangered!');
    }
  }
</script>
```

> jQuery에서는 parent(),parents(),closest()를 지원한다. 



