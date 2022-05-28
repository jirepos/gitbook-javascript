# Spread와  Rest 
ES6에 도입된 spread와 rest 정리한다. 

## Spread
constb는 consta의 속성을 필요로하고, constc는 constb의 속성을 필요로 할 때 기존의 문법에서는  아래과 같이 작성해야 한다.(다른 방법도 있지만)

```jsx
    const consta = { 
      name: '홍길동'
    }
    const constb = { 
      name : '홍길동',
      id : 'A01'
    }
    const constc = { 
      name: '홍길동', 
      id: 'A01',
      color : 'red'
    }
```


spread를 사용하면 다음과 같이 할 수 있다. 
```jsx
    const consta = { 
      name: '홍길동'
    }
    const constb = { 
      ...consta, 
      id : 'A01'
    }
    const constc = { 
      ...constb, 
      color : 'red'
    }
```
객체를 각 const를 확인해 보자. 
```jsx
    console.log(consta)
    console.log(constb)
    console.log(constc) 
```
```
{name: '홍길동'}
{name: '홍길동', id: 'A01'}
{name: '홍길동', id: 'A01', color: 'red'}
```

배열에도 적용할 수 있다. 
```jsx
    const animals = [ '개', '고양이', '사자'];
    const animals2 = [...animals, '기린'];
    console.log(animals);
    console.log(animals2);
```   

```
['개', '고양이', '사자']
['개', '고양이', '사자', '기린']
``` 


## rest 
### 객체에서의 rest
rest는 객체, 배열, 그리고 함수의 파라미터에서 사용이 가능하다. 
```jsx
    const objecta = { 
      name: '홍길동',
      color: 'red',
      age : 10 
    }

    const { color, ...obj } = objecta;
```    
결과를 확인해 보자. 

```jsx
    console.log(color)
    console.log(obj) 
```    
color는 red를 출력하고 obj는 color를 제외한 나머지가 할당된다. 
```
red
spread.html:42 {name: '홍길동', age: 10}
```
### 배열에서의 rest
이번에는 배열에서의 rest를 확인해 보자. 


```jsx
    const arr = [ 0,1,2,3];
    const [one, ...arr2] = arr; 
    console.log(one);
    console.log(arr2);    
```
one에는 0이 설정되고, arr2에는 나머지가 설정된다. 
```
0
[1, 2, 3]
```

### 함수 파라미터에서의 rest 

함수의 파라미터에서 rest 사용이 가능하다. 함수내에서는 배열로 받는다. 

```jsx
    function sum(...rest) {
      // 출력하면 배열임
      console.log(rest)   // [ 1,2,3,4]
      let hap = 0;
      for(var i=0; i < rest.length; i++) {
         hap = hap + rest[i]
       }
       return hap 
    }
    let result = sum(1,2,3,4)  // 갯수가 정해지지 않은 파라미터 전달
    console.log(result) 
```    
reduce를 사용하면 다음과 같이 함수를 작성할 수 있다. 
```jsx
return rest.reduce((acc, current) => acc + current, 0);
```






## References
[Spred 참고 사이트](https://learnjs.vlpt.us/useful/05-smarter-conditions.html)    
