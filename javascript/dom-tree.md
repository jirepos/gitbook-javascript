# DOM Tree

자바스크립트 기초강의 첫번째 자료로서 웹페이지의 문서구조를 표현하는 DOM에 대해서 알아본다. DOM은 문서를 논리 트리로 표현한다. 모든 HTML 요소는 HTML DOM을 통해 접근할 수 있다.

## Markup이란?

HTML은 Hyper Text Markup Language의 약자이다. Markup은 언어는 마크(Mark)로 둘러싸인 언어이다. 태그로 둘러싸여 있다고도 표현한다.

Hyper는 뛰어 넘다, 초월하다의 의미가 있다. Hyper text는 text를 뛰어 넘는다는 의미가 있다. 1990s년 Tim Berners-Lee는 웹(Web)에 대한 그의 비전의 일부로 하이퍼 텍스트의 개념을 정의했다. 그리고 SGML을 기반으로 하는 마크업(Markup)을 공식화 했다.

아래 그림은 하이퍼텍스트의 원리를 보여주는 간단한 구조의 예인데, A의 특정 부분을 읽다가 B로 가거나 D로 가거나, E로 가거나 할 수 있다.

![](<../.gitbook/assets/image (2).png>)



위 그림은 여섯개의 노드와 아홉개의 링크로 이루어진 하이퍼 텍스트의 구조를 표현한다.

## DOM

문서 객체 모델(The Document Object Model, 이하 DOM) 은 HTML, XML 문서의 프로그래밍 interface 이다. DOM은 문서의 구조화된 표현(structured representation)을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 그들이 문서 구조, 스타일, 내용 등을 변경할 수 있게 돕는다. DOM 은 구조화된 nodes와 property 와 method 를 갖고 있는 objects로 문서를 표현한다. 이들은 웹 페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 연결시켜주는 역할을 담당한다.

* DOM은 Document Object Model의 준말
* HTML 문서에 포함된 개개의 콘텐츠에 접근할 수 있게 API를 정의한 것
* 자바스크립트에서 HTML 문서의 요소나 속성에 접근하려면 DOM을 사용



![](<../.gitbook/assets/image (1).png>)



### 중요한 데이터 타입들

![](../.gitbook/assets/image.png)

#### Node

Node는 여러 가지 DOM 타입들이 상속하는 인터페이스이며 그 다양한 타입들을 비슷하게 처리할 수 있게 한다. 예를들어, 똑같은 메소드를 상속하거나 똑같은 방식으로 테스트를 할수있다

**프라퍼티**

| 속성              | 설명                             |
| --------------- | ------------------------------ |
| Node.childNodes | 이 노드의 모든 자식들을 포함하는 NodeList 반환 |
| Node.firstChild | 이 노드의 첫번짹 직접 작식 노드             |
| Node.lastChild  | 이 노드의 마지막 직접 자식 노드             |
| Node.nodeName   | Node의 이름                       |

Node의 firstChild 속성을 사용하여 node의 게층 구조를 이해하기 위한 간단한 예제 두 개를 살펴 볼 것이다.

> Node는 다루기 어렵기 때문에 잘 사용하지는 않는다. 이 문서에서는 Node의 속성을 통해 Node를 다루는 방법을 이해한다. 자세히 설명하지는 않는다.

#### Node 예제 1

```html
<p id="para-01">
  <span>First span</span>
</p>
```

```javascript
<script>
  window.addEventListener('load', function() {
    var p01 = document.getElementById('para-01');
    alert(p01.firstChild.nodeName)
  })
</script>
```

아래는 첫번째 예제의 마크업이다.

First span

***

window.addEventListener('load', function() { var p01 = document.getElementById('para-01'); //alert(p01.firstChild.nodeName) })

위에서, alert는 태그 \<p>의 끝과 여는 태그 \<span> 사이에 공백을 유지하여 삽입되었기 때문에 #text를 보여준다. space 하나에서 여럿, return, tab 등 어떤 공백이든 #text 노드에 삽입되게 된다.

#### Node 예제 2

```html
<p id="para-02"><span>First span</span></p>
```

```javascript
<script>
  window.addEventListener('load', function() {
    var p02 = document.getElementById('para-02');
    alert(p02.firstChild.nodeName)
  })
</script>
```

window.addEventListener('load', function() { var p02 = document.getElementById('para-02'); //alert(p02.firstChild.nodeName) })

아래는 두 번째 예제의 마트업이다.

Second span

위에서, alert는 태그 \<p>와 여는 태그 \<span> 사이에 공백이 없기 때문에 SPAN을 보여준다.

### DOM의 핵심 Interfaces

이 섹션은 DOM 에서 가장 많이 사용되는 interfaces 를 정리해보았다.

* document.getElementById(id)
* document.getElementsByTagName (en-US)(name)
* document.createElement(name)
* parentNode.appendChild (en-US)(node)
* element.innerHTML (en-US)
* element.style.left
* element.setAttribute (en-US)
* element.getAttribute
* element.addEventListener (en-US)
* window.content (en-US)
* window.onload (en-US)
* window.dump (en-US)
* window.scrollTo (en-US)
