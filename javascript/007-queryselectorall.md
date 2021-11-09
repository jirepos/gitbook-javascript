# querySelectorAll

Document에서 요소들을 선택하는 querySelectorAll() API에 대해서 알아본다.

## 요소와 속성 제어

DOM 요소를 선택하는 방법에 대해서 살펴본다.

### Selectors API

### document.querySelectorAll

Document 메소드 querySelectorAll() 는 지정된 셀렉터 그룹에 일치하는 다큐먼트의 엘리먼트 리스트를 나타내는 정적(살아 있지 않은) NodeList 를 반환한다. 선택자에 일치하는 요소가 하나도 없으면 요소의 수가 0인 NodesList 객체를 반환한다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Document</title>
  <script>
    window.addEventListener('load', function () {
      var spans = document.querySelectorAll("body>div>div>span")
      console.log(spans)
      for(var i=0; i < spans.length; i++) {
        console.log(spans.item(i))
        var span = spans.item(i)
        console.log(span.getAttribute("name"))
      }
    })
  </script>
</head>
<body>
  <div>
    <div>
      <span name="span1">111</span>
      <span name="span2">222</span>
    </div>
  </div>
</body>
</html>
```
