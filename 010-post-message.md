# PostMessage

- 페이지와 생성된 팝업 간의 통신
- 페이지와 페이지 안의 iframe 간의 통신

대체로, 

- 한 window는 다른 window를 참조할 수 있다. (targetWindow = window.openner)
- targetWindow.postMessage()를 통해 다른 window에 MessageEvent를 전송할 수 있다.

## 문법

```jsx
targetWindow.postMessage(mesage, targetOrigin, [transfer])
```

**message**

다른 window에 보내질 데이터 

**targetOrigin**

origin을 지정한다.  문자열 "*"이거나 URI이어야 한다. 

**transfer(Optional)**

일련의  Transfable 객체들.




## Dispatched event

아래의 JavaScript를 실행하면 otherWindow에서 전달된 메시지를 받을  수 있다. 

```jsx
window.addEventListener("message", receiveMessage, false);

function receiveMessage(event)
{
  if (event.origin !== "http://example.org:8080")
    return;

  // ...
}
```

전달된 메시지의 프러터피는 다음과 같다. 

**data**

다른 윈도우에서 온 오브젝트. 

**origin**

postMessage가 호출될 때 메시지를 보내는 윈도우 origin 

**source**

메시지를 보낸 window 오브젝트에 대한 참조 

## 메시지 보내고 자신이 수신하기

아래 코드는 자신에게 postMessage를 보내고 자신이 수신하고 있다. 

```jsx
<!DOCTYPE html>
<html lang="en">
  <head>
  </head>
  <body>
    <input id="btn" type="button" value="Click" />

    <script>
      var d = window.document;
      var btn = d.querySelector("#btn");
      btn.addEventListener("click", () => {
        window.postMessage("Hello", "*");
      });

      window.addEventListener("message", (evt) => {
        console.log(evt);
      });
      window.addEventListener("message", (evt) => {
        console.log("Me too");
      });
    </script>
  </body>
</html>
```

## 팝업윈도와 메인 윈도우 간의 메시지 전송

### Main 페이지

```jsx
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <script>
      let popup = window.open("/post-popup.html", "_blank", 'toolbar=0,location=0,menubar=0');
      window.addEventListener("load", () => {
        let btn = document.querySelector("#btn");
        //let popup;
        btn.addEventListener("click", () => {
          // popup이 완전히 로드되었을 때 postMessage가 가능하다 
          popup.postMessage("Hello", "*");
        });

        window.addEventListener("message", (evt) => {
          console.log(evt.origin);
          console.log(evt.source);
          console.log("====== Data");
          console.log(evt.data);
        }, false);
      });
    </script>
  </head>
  <body>
    <h1>Main</h1>
    <input id="btn" type="button" value="Open popup" />
  </body>
</html>
```

### 팝업 페이지

```jsx
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <script>
      window.addEventListener("message", (evt) => {
        console.log("onmessage occured.")
        evt.source.postMessage(
          "this messagg coming from the poupu window.",
          evt.origin
        );
      }, false);
    </script>
  </head>
  <body>
    <h1>Popup</h1>
  </body>
</html>
```

## References

[https://developer.mozilla.org/ko/docs/Web/API/Window/postMessage](https://developer.mozilla.org/ko/docs/Web/API/Window/postMessage)
