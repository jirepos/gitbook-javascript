# Link rel

HTML  요소는 현재 문서와 외부 리소스의 관계를 명시합니다. 는 스타일 시트를 연결할 때 제일 많이 사용하지만, 사이트 아이콘("파비콘"과 홈 화면 아이콘) 연결 등 여러가지로 쓰일 수 있습니다.

```markup
<link href="main.css" rel="stylesheet">
```

```markup
<link rel="icon" href="favicon.ico">
```

```markup
<link href="mobile.css" rel="stylesheet" media="screen and (max-width: 600px)">
```

## 스타일 시트 load 이벤트

```markup
<script>
function sheetLoaded() {
  // Do something interesting; the sheet has been loaded
}

function sheetError() {
  alert("An error occurred loading the stylesheet!");
}
</script>

<link rel="stylesheet" href="mystylesheet.css" onload="sheetLoaded()" onerror="sheetError()">
```

## Using HTML Imports

> 여러 문서에서 가능하다고 나와있기는 한데 실제 Chrome에서는 html imports가 동작하지 않았다. [크롬에서 제거되었다](https://www.chromestatus.com/feature/5144752345317376)고 한다.

HTML을 로드하기 위해서 link tag를 추가한다. index.html에 componnent.html을 추가하려면 다음과 같이 작성한다.

```markup
<link rel="import" href="component.html" >
```

일반적인 HTML 파일들과 마찬가지로 scripts, stylesheets, web fonts 등 어떤 리소스드 로드할 수 있다.

component.html

```markup
<link rel="stylesheet" href="css/style.css">
<script src="js/script.js"></script>
```

doctype, html, head, body는 필요하지 않다.

* import의 mimetype은 text/html 
* import link는 컨텐츠를 여기에 추가해 주세요를 의미하지 않는다. 

```markup
<head>
  <link ref="import" href="import.html">
</head>
```

브라우저에서 지원여부 확인

```javascript
let isSupported = 'import' in document.createElement('link');
```

## Reference

[https://developer.mozilla.org/ko/docs/Web/HTML/Element/link](https://developer.mozilla.org/ko/docs/Web/HTML/Element/link) [https://www.webcomponents.org/community/articles/introduction-to-html-imports](https://www.webcomponents.org/community/articles/introduction-to-html-imports)
