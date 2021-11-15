# WebCache


## Web Cache

클라이언트가 요청하는 html, image, js, css 등에 대해 첫 요청 시 파일을 내려 받아 특정 위치에 복사본을 저장하고 이후 동일한 URL의 Resource 요청은 다시 내려 받지 않고 저장한 파일을 사용하여 더 빠르게 서비스하기 위한 것이다. 

## 웹 캐시의 종류

### 브라우저 캐시

- 브라우저에 의해 내부 디스크에 캐쉬

### Proxy Caches

- Browser Cache와 동일한 원리로 동작하며 Client나 Server가 아닌 네트워크 상에서 동작

### Gateway Caches

- 서버 앞 단에 설치되어 요청에 대한 캐쉬 및 효율적인 분배를 통해 가용성, 신뢰성, 성능 등을 수행

## 캐시 적용하기

HTTP headers를 사용하여 캐시를 적용한다. 

- Last-Modifeid와 Etag가 동시에 있다면 ETag가 우선
- Expires와 Cache-Control도 마찬가지

Cache-Control은 하나의 값이 아니라 다양한 지시자를 콤마(,)를 이용하여 값을 전달할 수 있다. 
| 지시자 | 설명 |
|----|----|
|max-age=[sec]	|고정된 절대 시간이 아닌 요청 시간으로부터 상대적 시간.|
|public|	일반적으로 HTTP 인증이 된 상태에서 일어나는 응답은 자동으로 private가 된다. public을 명시적으로 설정하면 인증이 된 상태라도 캐시하도록 한다. |
|private|	특정 유저(사용자의 브라우저)만 캐시하도록 설정한다. |
|no-cache|	응답 데이터를 캐시하고 있지만 먼저 서버에 요청해서 유효성 검사를 하도록 강제한다.|
|no-store	|어떤 상황에서도 response 데이터를 저장하지 않는다. |



> Pragma는 response에 대한 HTTP 명세가 없다. 단지 request에서 만 사용될 수 있으며 몇몇 캐시는 이 헤더에 의해 처리될 수 있지만 대부분은 처리되지 못하므로 사용하지 않는 것이 좋다.
> 

## 캐시 동작 방식

### 첫 요청

- 파일을 요청한다
- 브라우저에게 파일을 header와 함께 전달한다.
- 브라우저가 헤더의 내용에 따라 캐시 정책을 수행한다.

### 재 요청

**LAST-MODIFIED**

- 브라우저는 최초 응답 시 받은 Last-Modifeid 값을 If-Modified-Since라는 헤더에 포함하여 파일을 요청한다.
- 서버는 요청 파일의 수정 시간을 If-Modifeid-Since와 비굥하여 동일하면 304 Not Modified로 응답하고 다르다면 200 OK와 함께 새로운 Last-Modified 값을 응답 헤더에 전송
- 브라우저가 응답 코드가 304인 경우에 캐시에서 페이지를 로드하고 200이라면 새로운 파일을 받은 후 Last-Modified 값을 변경한다.

**ETAG(Entity Tag)**

- 브라우저는 Etag 값을 If-None-Match 헤더에 포함하여 파일을 요청
- 서버는 Etag 값을 If-None-Match 값과 비교하여 동일하다면 304 Not Modified로 응답하고 다르면 200 OK와 함께 새로운 Etag 값을 응답 헤더에 전송
- 응답 코드가 304인 경우에 캐시에서 페이지를 로드, 200이라면 새로 파일을 받은 후 Etag 값을 갱신

**Expires**

- 브라우저는 최초 응답 시 받은 Expires 시간을 비교하여 기간 내라면 서버를 거치지 않고 바로 캐시에서 페이지를 로드, 기간이 만료되었다면 위에서 언급한 Validation을 수행

**Cache-Control**

- 최초 응답 시 받은 Cache-Control 중 max-age 값을 GMT와 비교하여 기간 내라면 캐시에서 로드, 만료되었다면 validation 작업을 수행

> 시간은 HTTP date 형태이며 로컬 타임이 아닌 GMT를 사용한다.
> 

## 캐시 설정 방법

- 캐시는 서버에서 설정한다. 파일 확장자 명으로 다르게 설정하거나 디렉터리 별로 다르게 설정 할 수 있다.
- Expires나 Etag는 서버 설정에 의해 사용하지 않을 수 있다.
- expires가 설정되면 Expires와 max-age가 같이 설정된다.

### 캐시 전략

- 일관된 URL 사용
- 다운 가능한 파일의 내용이 바뀌면 URL을 바꾼다.
- SSL을 최소화 한다. (암호화된 페이지는 캐시 되지 않는다.)

## 브라우저의 두 가지 요청 유형

상황에 따라 두 가지 유형의 request를 보낸다. 

### Unconditional(download)

- 브라우저가 캐시된 파일을 가지고 있지 않는 경우
- 유저가 Ctrl + F5을 하는 경우
- 링크, 이전 & 다음 버튼, 주소창에 입력후 엔터를 치는 경우(이 때 fresh한 캐시 아이템이 서버와 통신 없이 캐시만으로 처리된다. )

### Conditional(validate)

Conditaion Request가 발생하면 요처되는 모든 Resource에 대해 freshness 여부에 상관없이 무조건 revalidation을 요청한다. 즉, freshness가 유효하다 하여도 서버 통신을 통해  304 또는 200의 응답을 받는다. 

- Cache-Control 또는 Expires가 만료된 경우
- META-TAG를 이용한 refresh 가 발생한 경우
- 자바스크립트의 location을 통해 reload가 된 경우
- cross-host HTTPS를 통해 요청되는 경우
- 유저가 새로고침을 하는 경우

## Heuristic expiration

Expired 또는 Cache-Control을 설정하지 않았는데 freshness가 유효하다 판단하여 서버에 요청하지 않고 캐시되는 경우가 있다.  Last-Modified가 명시된 경우 브라우저는 Heuristic expiration times를 부여한다. (브라우저마다 다르다)  

> 가능한 한 origin server에서 명확하게 expiration times를 명시하는 것이 좋다.
> 

## CONTENT-LENGTH IN RESPONSE HEADER

HTTP 1.1에서는 TCP/IP 커넥션이 끊어지지 않고 유지되는 Keep Alive connection(persistent connection)이 지원된다. response header에 content-length 항목이 추가 되면 이 기능이 활성화 되어 각 request를 위해 매번 설정하고 연결을 맺고 끊는 과정 없이 하나의 커넥션으로 전부 요청하기 때문에 페이지의 속도가 빨라진다. 

## Cache-Control

### 캐싱 막기

```jsx
Cache-Control: no-cache, no-store, must-revalidate
```

### 정적 에셋 캐싱

변경되지 않을 애플리케이션 내 파일들에 대해, 보통 적극적인 캐싱을 추가할 수 있습니다. 이것은 예를 들자면, 이미지, CSS 파일 그리고 자바스크립트 파일과 같이 애플리케이션에 의해 서브되는 정적 파일들을 포함합니다. 추가로, `Expires` 헤더를 참고하시기 바랍니다.

```jsx
Cache-Control:public, max-age=31536000
```

## 참고

[https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Cache-Control](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Cache-Control)