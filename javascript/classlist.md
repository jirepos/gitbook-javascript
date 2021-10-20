# classList

이 문서에서는 요소의 class 속성값을 제어하는 classList함수에 대해서 알아본다.

### 요소와 속성 제어

HTMl 5에서는 class 속성 값을 제어하는 API를 새로 규정했다. 매우 편리한 기능이니 알아두면 좋다.

### element.classList

```html
<!DOCTYPE html>
<html lang="en">
<head>
 <title>Document</title>
 <script>
   window.addEventListener('load', function() {
     let span1 = document.getElementById("span1")
     let tokenList = span1.classList 
     console.log(tokenList)
     for(let i=0; i < tokenList.length; i++) {
       let token = tokenList.item(i)
       console.log(token)
     }
     if(tokenList.contains('bbb')) { 
       console.log("the class 'bbb' is contained.")
     }
   })
 </script>
</head>
<body>
  <span id="span1"class="aaa bbb ccc" >
    여기
  </span>
</body>
</html>
```
