# Message Channel

## 메인 윈도우에서 채널 만들기

### MessageChannel
Channel Messaging API 의 MessageChannel인터페이스 를 사용하면 새 메시지 채널을 만들고 두 MessagePort 속성을 통해 이를 통해 데이터를 보낼 수 있다. 

#### Properties 
데이틀 보내고 받기 위한 두개의 port를 제공한다. port1과 port2는 읽기 전용이다. 한 포트는 메시지를 보내고 한 포트는 도착하는 메시지를 수신 대기한다. 

**MessageChannel.port1**
읽기 전용. 
**MessageChannel.port2**
읽기 전용. 



#### 생성하기 
```javascript
var channel = new MessageChannel();
```

#### 메시지 전송 
iframe에게 메시지를 전송하려면 postMessage()를 사용한다.  iframe이 로드되면 MessageChannel.port2를 사용하여 iframe에 메시지를 전달 할 수 있다. 
```javascript
iframe.contentWindow.postMessage('Hello from the main page!', '*', [channel.port2]);
```

**Parameters**
* message
채널을 통해 보내려고 하는 메시지. 기본타입일 수도 있고 배열일 수도 있다. 
* targetOrigin 
보내고자 하는 위치. "example.com" 처럼 도메인 오리진을 입력한다.  주소를 설정할 때 "*"을 사용하면  열려 있는 모든 탭과 iframe에 정보를 보낼 수 있다.  **보안상 취약하다.**
* transferList
optional이다. 전송 가능한 객체(Transferable) 인터페이스를 배열로 넘긴다. MessageChannel 생성자에 의해 생성된 port2를 다른 브라우징 컨텍스트에 넘겨주기 위한 용도이다. 넘겨준 이후에는 port2 의 소유권이 다른 브라우징 컨텍스트에 완전히 넘어가기 때문에, 현재 브라우징 컨텍스트 내에서 더 이상 사용할 수 없다.


**MessageChannel을 사용할 때 postMessage를 사용하는 이유**
> 통신을 위한 MessageChannel 을 만들었지만  port2 의 정보를 어떻게든 다른 브라우징 컨텍스트에 넘겨주어야 한다.  그래서 최초 1회에 한해서 postMessage로 port2 를 넘겨주게 된다. 그 후에는 port1과 port2 가 연결되었기 때문에, 더 이상 window.postMessage에 의존하지 않고 독자적인 메시지 채널을 통해 커뮤니케이션이 가능해진다. 


#### 메시지 수신 
iframe을 포함하는 window가 있으면 iframe으로 부터 오는 메시지를 수신할 수 있다. iframe으로 부터 오는 메시지를 수신하려면 port1을 사용한다. message  이벤트는 MesagePort 객체가 메시지를 수신할 때 발생된다. onmessage를 통해서 이용가능하다. 

```javascript
var channel = new MessageChannel();
channel.port1.onmessage = (message) => {

}
```


## IFrame에서 메시지 수신 및 발송 
iframe에서 메시지를 수신하려면 window.onmessage 핸들러를 사용한다. 
```javascript
window.addEventListener("message", (e) => {
  // do something 
});
```      
메인 페이지에게 메시지를 전달하려면 다음과 같이 작성한다. 
```javascript
window.addEventListener("message", (e) => {
  e.ports[0].postMessage("Message back from the IFrame");
});
```
이전에 우리는 port2를 ifrmae으로 이전(transfer)했다.  이것은 이벤트 속성(배열 위치[0])에서 엑세스 할 수 있다. 이것은 IFrame에 의해 제어되고 메시지 채널에 의해 port1에 연결되기 때문에 지정된 메시지가 기본 페이지로 다시 전송된다. 


## 메인페이지와 IFrame간의 메시지 송수신
앞에서 설명한 window.addEventListener(message)는 최초에 메인 페이지와 IFrame의 채널 연결을 하기 위한 이벤트 핸들러이고 지속적으로 메시지를 주고 받으려면 메시지 port1과 port2의 onmessage 이벤트 핸들러를 구현해야 한다. 

### 메인페이지에서 메시지 전달하기 
port1.postMessage()를 이용하여 메시지를 전달한다. 
```javascript
channel.port1.postMessage("나야나");
```

### IFrame에서 메시지 수신 
window.onmessage 이벤트 핸들러의 파라미터의 event 객체의 ports[0]의 onmessage 핸들러를 구현해야 한다. 

```javascript
      window.addEventListener("message", (e) => {
        // 계속 메시지를 수신하려면 port1.onmessage를 구현해야 함
        e.ports[0].onmessage = (e) => {
          log(e.data);
        };
      });

```        


### 전체코드 
#### 메인 페이지
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <h1>ChannelMessage</h1>
    <div class="output"></div>
    <input id="btnSend" type="button" value="sendMessage" />
    <iframe id="iframe" src="./sub.html" frameborder="0"></iframe>
    <div id="log"></div>
    <script>
      // https://developer.mozilla.org/ko/docs/Web/API/Channel_Messaging_API/Using_channel_messaging
      var channel = new MessageChannel();

      const log = (message) => {
        var log = document.querySelector("#log");
        var ele = document.createElement("div");
        ele.innerHTML = message;
        log.appendChild(ele);
      };
      //log("script started.");
      var iframe = document.querySelector("#iframe");
      iframe.addEventListener("load", () => {
        //log("iframe loaded.");
        iframe.contentWindow.postMessage("Hello from the main page!!!!", "*", [
          channel.port2
        ]);
        channel.port1.onmessage = (e) => {
          //log("onmessage");
          //log("<strong>received from ths other window");
          log(e.data);
        };
      });
      var btn = document.querySelector("#btnSend");
      btn.addEventListener("click", () => {
        //log("clicked");
        channel.port1.postMessage("나야나");
      });
    </script>
  </body>
</html>
```

#### subpage 
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <h1>IFRAME</h1>
    <div class="output"></div>
    <script>
      const log = (message) => {
        var log = document.querySelector(".output");
        var ele = document.createElement("div");
        ele.innerHTML = message;
        log.appendChild(ele);
      };
      window.addEventListener("load", () => {
        // Use the transfered port to post a message back to the main frame
        //e.ports[0].postMessage('Message back from the IFrame');
      });
      var output = document.querySelector(".output");
      // window.onmessage는 최초 채널에 참여하기 위한 용도
      window.addEventListener("message", (e) => {
        //console.log("meeesage");
        output.innerHTML = e.data;
        e.ports[0].postMessage("Message back from the IFrame");
        // 계속 메시지를 수신하려면 port1.onmessage를 구현해야 함
        e.ports[0].onmessage = (e) => {
          log(e.data);
        };
      });
    </script>
  </body>
</html>
```


















## Reference 
[https://developer.mozilla.org/ko/docs/Web/API/Channel_Messaging_API/Using_channel_messaging](https://developer.mozilla.org/ko/docs/Web/API/Channel_Messaging_API/Using_channel_messaging)
[https://developer.mozilla.org/en-US/docs/Web/API/MessagePort](https://developer.mozilla.org/en-US/docs/Web/API/MessagePort)
[https://wormwlrm.github.io/2020/11/29/Communicate-with-iframe-via-Message-Channel-API.html](https://wormwlrm.github.io/2020/11/29/Communicate-with-iframe-via-Message-Channel-API.html)






