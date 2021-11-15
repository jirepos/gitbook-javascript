# JavaScript Class

## 지원 브라우저

- Chrome
- Edge
- Firefox
- safari iOS
- Node.js
- Chrome Android
- Safari


## 기본 구조 
```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <script>
      class Person {
        constructor(name, age) {
          // 인스턴스 속성은 반드시 클래스 메서드 내에 정의되어야 합니다:
          this._name = name; // instance 변수, getter/setter와 이름이 같지 않아야 한다.
          this._age = age; // 이름이 같으면 무한 루프
        }
        // getter
        get age() {
          return this._age;
        }
        // setter
        set age(value) {
          this._age = value;
        }
        // method
        walk() {
          console.log(this._name);
        }

        // static member
        static displayName = "Person's Name";
        static getDisplayName() {
          //return Person.displayName; // Person 클래스명. 을 붙이거나 this. 을 붙여야
          return this.displayName;
        }

        // this
        speak() {
          return this; // Person 인스턴스 객체를 가리킨다.
        }
        static eat() {
          return this; // Person class를 가르킨다
        }
      }

      let person = new Person("Hongil", 20);
      person.age = 30;
      console.log(person.age);
      person.walk();
      console.log(Person.displayName); // 정적 필드 호출
      console.log(Person.getDisplayName()); // 정적 메서드 호출
      console.log(Person.eat()); // Person Class
      console.log(person.speak()); // Person 인스턴스 객체
    </script>
  </body>
</html>


```


## Field 
```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <script>
      class Person {
        name = ""; // public field
        age = 0;
        // 일반적인 프로퍼티와는 다르게 private 필드는 값을 할당하면서 만들어질 수 없습니다.
        #address; // private field
        constructor(name, age, address) {
          this.name = name;
          this.age = age; // public field
          this.#address = address; // private field
        }
        speak() {
          console.log(this.#address); // private field 사용
        }
      }

      let person = new Person("Hongil", 20, "Pusan");
      this.name = "Kim";
      console.log(person.name);
      console.log(person.address); // undefined
      person.speak(); // Pusan
    </script>
  </body>
</html>
```

## 상속 

```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <script>
      class Animal {
        constructor(name) {
          this.name = name;
        }

        speak() {
          console.log(`${this.name} makes a noise.`);
        }
      }

      class Dog extends Animal {
        constructor(name) {
          // subclass에 constructor가 있다면, "this"를 사용하기 전에 가장 먼저 super()를 호출해야 합니다.
          super(name); // super class 생성자를 호출하여 name 매개변수 전달
        }

        speak() {
          console.log(`${this.name} barks.`);
          // super.speak()를 사용하면 부모의 speak() 호출
        }
      }

      let d = new Dog("Mitzie");
      d.speak(); // Mitzie barks.
    </script>
  </body>
</html>
```
