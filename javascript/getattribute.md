# getAttribute

이 문서에서는 DOM 요소를 속성을 가져오는 getAttribute() 함수에 대해서 알아본다.

## 요소와 속성 제어

요소의 속성을 가져오는 API를 알아보자.

### getAttribute()

```html
<!DOCTYPE html>
<html lang="en">
<head>
 <title>Document</title>
 <script>
   window.addEventListener('load', function() {
     let apple = document.getElementById("apple")
     console.log(apple.getAttribute('value'))
     console.log(apple.getAttribute('id'))
     console.log(apple.getAttribute('type'))
   })
 </script>
</head>
<body>
  <form>
    <input id="pear"type="text"  value="This is a pear.">
    <input id="apple"type="text" value="This is an apple.">
  </form>
</body>
</html>
```
