# 요소와 속성 제어

DOM 요소를 선택하는 방법에 대해서 살펴본다.

## Selectors API

## document.querySelector

선택자와 일치하는 요소 중 가장 첫 번째로 발견된 요소의 노드 객체를 반환한다. 일치하는 요소가 없으면 null을 반환한다.

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

## Referencese

querySelector() 함수의 매개 변수인 선택자 패턴은 첨부된 files/CSS selectors cheatsheet.pdf 파일을 참고한다.
