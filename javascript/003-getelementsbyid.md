# getElementsById

이 문서에서는 DOM 요소를 가져오는 getElementsById() 함수에 대해서 알아본다.

## 요소와 속성 제어

ID 속성으로 요소를 가져오는 API를 살펴볼 것이다. ID는 name과 달리 전체 트리에서 유니크해야 한다.

### document.getElementById()

```html
<!DOCTYPE html>
<html lang="en">
<head>
 <title>Document</title>
 <script>
   window.addEventListener('load', function() {
     let apple = document.getElementById("apple")
     console.log(apple)
     console.log(apple.value)
   })
 </script>
</head>
<body>
  <form>
    <input id="pear"type="text"  value="pear">
    <input id="apple"type="text" value="apple">
  </form>
</body>
</html>
```
