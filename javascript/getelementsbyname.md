# getElementsByName

이 문서에서는 DOM 요소를 가져오는 getElementsByName() 함수에 대해서 알아본다.

## 요소와 속성 제어

웹 애플리케이션을 제작할 때 요소나 속성을 제어하는 경우가 많다. 자주 사용하는 API를 살펴보자. 먼저 tag의 이름 속성으로 요소를 가져오는 api를 알아 보겠다.

### document.getelementsByName(“name”)

```html
<!DOCTYPE html>
<html lang="en">
<head>
 <title>Document</title>
 <script>
   window.addEventListener('load', function() {
     let elements = document.getElementsByName('fruits')
     console.log(elements)
     for(var i=0; i < elements.length; i++) {
       console.log(elements[i].name)
     }
   })
 </script>
</head>
<body>
  <form>
    <input name="fruits" type="text">
    <input name="fruits" type="text">
    <input name="fruits" type="text">
    <input name="fruits"type="text">
  </form>
</body>
</html>
```
