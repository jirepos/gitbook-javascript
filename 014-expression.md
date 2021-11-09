# JavaScript 고급 표현식

## ||  사용 
아래는 if를 사용하여 분기 처리했다. 
```javascript

    function setTitle(title) {
      if(!title) {
        return "Untitled";
      }else  {
        return title;
      }
    }
    let title = setTitle("111");
    console.log(title);
```

|| 연산자를 사용하여 간단히 처리할 수 있다. 
```javascript
    let title2 = "" || "Untitled";
    console.log(title2);
```


## && 사용 
if를 사용하여 분기처리한 함수를 보자.
```javascript
    function isAdult(age) { if (age && age > 17) { return true; } else { return false; } }
    let adultState = isAdult(0)
    console.log(adultState);
```
&&를 사용하여 간단히 처리할 수 있다. 
```javascript
    function isAdult2(age)  { return (age && age > 17)? true: false;}
    let adultState2 = isAdult2(0);
    console.log(adultState2);
```


##  && 사용 분기처리를 간단히 
분기처리된 함수를 사용한 예를 보자. 
```javascript

    // 분기처리하여 함수 호출
    function getUserId(user) {
      if(user && user.id) {
        return user.id; 
      }else {
        return null;
      }
    }
    let user = null; 
    let userId = getUserId(user);
    console.log(userId); 
    // 간단히 

```
다음과 같이 간단히 표현할 수 있다. 

```javascript
    let userId2 = (user && user.id) || null;
    console.log(userId2);
```


## 즉시 실행 함수 
함수가 여러 고셍서 사용되지 않은면 즉시 실행함수를 사용하여  간단히 표현할 수 있다. 
```javascript
   // 즉시 실행 함수 
    let userId3 = (user && user.id) || ( function() { return  "Relogined" })();
    console.log(userId3); 
```
이것을 arrow function을 사용하여 더 간단히 표현할 수 있다. 
```javascript
    let userId4 = (user && user.id) || ( () => "Relogined" )();
    console.log(userId3); 
```
