# 사용자 정의 속성

이 문서에서는 요소에 사용자가 속성을 정의하는 방법에 대해서 알아본다.

### 요소와 속성 제어

속성명 앞에 data-를 붙인 다음에 선호하는 이름의 속성 요소를 마크업할 수 있다.

## custom data

```html
<!DOCTYPE html>
<html lang="en">
<head>
 <title>Document</title>
 <script>
   window.addEventListener('load', function() {
     let span1 = document.getElementById("span1")
     console.log(span1.dataset.resource)
     console.log(span1.dataset.totalNum)
     console.log(span1.dataset['totalNum']) // 지원
     console.log(span1.dataset['total-num']) // 지원하지 않음
     console.log(span1.getAttribute('data-total-num'))  // getAttribute() 사용예
   })
 </script>
</head>
<body>
  <span id="span1" data-resource="custom.txt" data-total-num="6" >
    여기
  </span>
</body>
</html>
```
