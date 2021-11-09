# Base64

## encodeURIComponent()

이 함수는 URI의 특정한 문자을 UTF-8로 인코딩한다. 다음 문자을 제외한 문자를 이스케이프한다. URI 인코딩은 나머지 문자들을 옥텟 단위로 묶어서 16 진수 값으로 인코딩한다.

```
A-Z a-z 0-9 - _ . ! ~ * ' ( )
```

예를 들어 사용자가 입력한 "Jack & Jill"은 "Jack \\& Jill"로 인코딩 된다. GET과 POST에서는 "&", "+", "="를 특별한 문자로 취급한다.

예를 들어 공백(space)는 '%20'으로 치환된다. '&'은 '%26'으로 치환된다.

| 문자 | URL 인코딩 | 문자 | URL 인코딩 |     |
| -- | ------- | -- | ------- | --- |
| 탭  | 9%      | ?  | %3F     |     |
| 공백 | 20%     | @  | 40%     |     |
| !  | 21%     | ^  | %3E     |     |
| "  | 22%     | {  | %7B     |     |
| #  | 23%     | }  | %7D     |     |
| %  | 25%     | \[ | %5B     |     |
| &  | 26%     | ]  | %5D     |     |
| (  | 28%     | \` | 60%     |     |
| )  | 29%     |    |         | %7C |
| +  | %2B     | \~ | %7E     |     |
| \\ | %5C     |    |         |     |
| ,  | %2C     |    |         |     |
| .  | %2E     |    |         |     |
| /  | %2F     |    |         |     |
| :  | %3A     |    |         |     |
| ;  | %3B     |    |         |     |
| <  | %3C     |    |         |     |
| >  | %3E     |    |         |     |
| =  | %3D     |    |         |     |

인코딩과 디코딩을 해주는 함수는 다음과 같다.

* encodeURI( uri ) : URI에서 자주 사용하는 : ; / = ? & 등을 \* 제외하고 인코딩하는 함수
* encodeURIComponent( uri ) : 모든 문자를 인코딩하는 함수
* decodeURI( uri ) : encodeURI의 결과물을 디코딩하는 함수
* decoudeURIComponent ( uri ) : encodeURIComponent의 결과물을 디코딩하는 함수

## escape()/unescape()

escape() 함수는 아스키 문자에 해당되지 않는 것을 모두 유니코드 형식으로 변환해 준다. 16진수 형태로 바꾸는 것이다. 표기법은 1 바이트일 때 %XX 이며, 2 바이트일 때에는 %uXXXX이다. 앞에 u가 하나 더 붙는다.

인코딩한 문자열을 다시 원래대로 되돌리고 싶다면 디코딩을 해야 한다. 디코딩 함수는 unescape()이다.

## BASE64 처리

ASCII 문자만 있는 문자열의 경우에는 btoa(), atob()를 그냥 사용해도 된다. 하지만 한글과 같은 ASCII 문자 이외의 문자를 포함한 문자열은 encoding과 decoding을 할 수 없다. 한글과 같은 문자를 포함한 문자열을 BASE64로 인코딩과 디코딩을 하려면 위에서 설명한 함수들을 혼용해서 사용해야 한다.

### encoding

문자열을 encodeURIComponent()로 감싸고 그것을 다시 unescape()로 감싼다.

```javascript
var encodedStr = btoa(unescape(encodeURIComponent(txtContent.value)))
```

### decoding

디코딩은 인코딩의 역순으로 감싼다.

```javascript
var decodedStr = decodeURIComponent(escape(window.atob(txtEncoded.value)))
```

위 방법으로 매번 코딩을 하기에는 어려움이 있기 때문에 공통함수를 만들어서 처리한다.

```javascript
// Base64.js

const Base64 = { 

  encode(strToEncode) {
    return btoa(unescape(encodeURIComponent(strToEncode)));
  },
  decode(strToDecode) {
    return decodeURIComponent(escape(window.atob(strToDecode)))
  }
}
```
