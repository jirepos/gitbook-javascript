# 객체 리터럴

## this에 대해서

객체 리터럴에서 this는 자기 자신을 의미한다. 

```jsx

var user = { 
  name: "Hong", 
  print() {
    console.log(this.name);  // this는 user를 가르킨다. 
  }
}

user.print();  // '홍'이 출력된다.
```

자기 자신에게 선언된 함수를 호출할 때에도 this를 사용한다. 

```jsx
var user = { 
  name: "Hong", 
  age:   10 , 
  printAge() {
    console.log(this.age);
  }, 
  print() {
    console.log(this.name);  // this는 user를 가르킨다. 
  },
  callPrintAge() {
    this.printAge();  // printAge()를 호출
  }
}

user.print();  // '홍'이 출력된다. 
user.callPrintAge(); // 10이 출력된다.
```

### 객체 안의 객체에서의 this

객체 안에 fn이라는 객체를 만들고 함수를 하나 정의한다. 그 함수를 호출해 보자. 

```jsx
var user = { 
  name: "Hong", 
  fn: {
    testA()  {
      console.log(this.name)  // undefined
    },
  }
}

user.fn.testA();
```

그러면 undefined가 출력된다. 참조할 수가 없다는 의미이다. 이때는 user.name으로 name 속성을 참조해야 한다. 

```jsx
var user = { 
  name: "Hong", 
  fn: {
    testA()  {
      console.log(user.name)  // undefined
    },
  }
}

user.fn.testA();
```

함수 또한 마찬가지이다.  this 말고 user를 사용해야 한다. 

```jsx
var user = { 
  name: "Hong", 
  print() {
    console.log(this.name);
  },
  fn: {
    testA()  {
      user.print();
    },
  }
}

user.fn.testA();
```

### 객체 안의 객체에서의 this

객체 안의 fn에서 this.fn.testA()와 같이 호출하면 오류가 발생한다. 

```jsx
var user = { 
  fn: {
    
    testA()  {
      console.log("testA")
    },
    testB() {
      this.fn.testA();
    }
  }
}

user.fn.testB();
```

다음과 같이 this.testA()와 같이 this를 바로 사용해야 한다. 

```jsx
var user = { 
  fn: {
    
    testA()  {
      console.log("testA")
    },
    testB() {
      this.testA();
    }
  }
}

user.fn.testB();

```