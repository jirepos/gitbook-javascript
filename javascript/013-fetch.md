# Fetch()


Fetch의 기본 스펙은 jQuery.ajax()와 기본적으로 다르다. 

* HTTP Statue Code가 404나 400을 반환하더라도 HTTP error 상태를 reject()하지 않는다. 
* 네트워크 장애나 요청이 완료되지 못한 상태에서는 reject()가 반환된다. 
* 쿠키를 보내거나 받지 않는다. 
* 쿠키를 전송하기 위해서는 자격증명(credentials) 옵션을 설정해야 한다. 



**기본 코드** 
```jsx
fetch('http://example.com/movies.json')
  .then(function(response) {
    // Respnose.json()을 사용하여 json 반환 
    return response.json();
  })
  .then(function(myJson) {
    // JSON 객체를 인자로 받음 
    // 문자열로 변환하여 출력
    console.log(JSON.stringify(myJson));
  });
```




