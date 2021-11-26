# 배열 다루기 

## forEach
forEach는 가장 기본적인 Loop 메소드이다.  

**형식**
```
arr.forEach(callback(currentvalue[, index[, array]])[, thisArg])
```

* currentValue: 배열에서 현재 처리 중인 요소.
* index: 배열에서 현재 처리 중인 요소의 인덱스.
* array: forEach()가 적용되고 있는 배열.

**예제**
```jsx
    /// forEach
    let arr = [1,2,3,4,5]
    arr.forEach( e => {
      console.log(e)
    })
```
결과값은 다음과 같다. 
```shell
1
2
3
4
5
```

## map() 
map 메소드는 요소를 일괄적으로 변경하는데 사용한다. 
```jsx
   var firstNames = ['kim', 'hong', 'park'];
   var convertedArr = firstNames.map( e => {
     return "F" + e; 
   })
   console.log(convertedArr); 
```

```
['Fkim', 'Fhong', 'Fpark']
```


## filter() 
filter는 걸러주는 역할을 한다. 콜백 함수는 리턴은 boolean을 가진다. 리턴이 true인 요소만 모아서 새로운 배열을 만든다. 


```jsx
const numbers = [1, 2, 3, 4, 5]; 
const result = numbers.filter(number => number > 3); 
console.log(numbers); // [1, 2, 3, 4, 5]; 
console.log(result);  // [4, 5]
```



## find()
find 메소드는 filter와 비슷하지만 단 하나의 요소만 리턴한다. find는 콜백 함수의 리턴이 true인 요소를 찾을 떄 까지 순회하다가 찾으면 거기서 끝난다. 만약 발견하지 못하면 undefined가 반환된다. 

```jsx
    // find
    let numArr = [1, 200, 300, 400];
    var retArr = numArr.find( e => {
        return e % 5 == 0;
    }); 
    console.log(retArr); // 15
```
결과 값은 
```shell
200
```



## reduce() 
나중에 정리하기로 한다. 

