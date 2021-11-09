# window.open 팝업으로 열기 

## 문법 
```jsx
var newWin = window.open(url, name, specs, replace)
```

**name**
- _blank : 새 창에 열립니다. 이것이 기본값입니다.
- _parent : 부모 프레임에 열립니다.
- _self : 현재 페이지를 대체합니다.
- _top : 로드된 프레임셋을 대체합니다.
- name(임의의 이름) : 새 창이 열리고 창의 이름을 지정합니다. 동일한 이름에 다시 open() 을 하면 기존의 열린창의 내용이 바뀝니다. 다른 이름을 사용하면 또다른 새창이 열립니다.


**replace**
히스토리 목록에 새 항목을 만들지 현재 항목을 대체할지 지정한다. 
- true : 현재 히스토리를 대체합니다.
- false : 히스토리에 새 항목을 만듭니다.



## 새로운 탭으로 열기 
```jsx
function NewTab() { 
            window.open( 
              "https://www.yourURL.com", "_blank");
}
```
## Popup으로 열기 
```jsx
//open in new window, not new tab
window.open('https://www.codegrepper.com', '_blank', 'toolbar=0,location=0
```

