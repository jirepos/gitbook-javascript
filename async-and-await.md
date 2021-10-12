# Async and Await

async function은 async 키워드로 선언된다. 그리고 await keyword가 그것 안에 허락된다. async와 await는 비동기적, promise-based 동작을 가능하게 한다.

```javascript
let hello = async function() { return "Hello" };
hello().then( (value) => { 
    console.log(value);
})
```

async 를 함수와 같이 사용하면 결과를 직접 반환하는게 아니라 Promise를 반환하게 한다.

await는 async function 안에서만 쓸 수 있다. await 키워드는 JavaScript 런타임이 이 라인에서 비동기 코드를 일시 중지하여 비동기 함수 호출이 결과를 반환할 때 까지 기다리게 한다.

```javascript
 async function myFetch() {
  let response = await fetch('coffee.jpg'); // 비동기로 실행하는 것이 아니라 기다린다. 
  let myBlob = await response.blob();

  let objectURL = URL.createObjectURL(myBlob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
}
```

myFetch() 함수 내에 코드가 이전의 Promise버전과 매우 유사하지만, 다른점이 있다. then()블럭을 사용하여 작업을 이어가는 대신 메서드 호출 전에 await 키워드를 사용하여 반환된 결과를 변수에 할당한다. await 키워드는 JavaScript 런타임이 이 라인에서 비동기 코드를 일시 중지하여 비동기 함수 호출이 결과를 반환할 때 까지 기다리게 한다.

아래는 원래의 fetch() 함수이다.

```javascript
fetch('coffee.jpg')
.then(response => response.blob())
.then(myBlob => {
  let objectURL = URL.createObjectURL(myBlob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
})
.catch(e => {
  console.log('There has been a problem with your fetch operation: ' + e.message);
});
```
