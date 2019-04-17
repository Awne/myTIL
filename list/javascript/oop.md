## this

`this`를 변경하기 위해 `call` `apply` `bind` 를 사용할 수 있음.

`bind`는 값을 호출하지 않고 정의만 함.

함수의 인자를 담는 `arguments`는 유사배열이기에 배열 메소드를 사용할 수 없음.

```javascript
function example() {
    console.log(arguments.join());
} 

example(1,'string',true);   // 에러발생
```
`call` 메소드를 사용한다.
```javascript
function example() {
    console.log(Array.prototype.join.call(arguments));
}

example(1,'string',true);   // 출력
```

참고로 `arguments`의 부모는 `arguments.callee`로 호출한다.

## 객체 인스턴스 생성 방법

1. 생성자 함수 사용

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

let Jun = new Person('Jun',20);
```
2. Object 생성자 사용

```javascript
let Jun = new Object();
Jun.name = "Jun";
Jun.age = 20;
```
3. Object.create 메소드 사용

```javascript
let Jun = Object.create(Person);
```

## 상속

`Person`을 상속받고 `subject`프로퍼티를 가지며, `greeting`메서드를 추가한 `Teacher`클래스

```javascript
function Teacher(subject) {
    Person.call(this, name, age);
    this.subject = subject;
}

Teacher.prototype = Object.create(Person.prototype)
// 메소드 상속
```
위 메소드 상속으로 인해 `Teacher.prototype.constructor`가 `Person()`이 됨.

이를 막기위해 아래 코드를 명시해줌.
```javascript
Teacher.prototype.constructor = Teacher; 
```

메소드를 추가하기 위해
```javascript
Teacher.prototype.greeting = function() {}
```

생성자간 상속도 가능함. 아래 코드는 `Bio`생성자를 상속받는 `People`생성자
```javascript
People.prototype = new Bio();
let marine = new People();

// 변수 marine은 People, Bio의 프로퍼티 및 메소드 사용가능
```

## 클래스

ES6, 간단한 인스턴스 생성, 상속

### 클래스를 통한 인스턴스 생성

```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    greeting() {}
}

let Jun = new Person("Jun", 20);
```

### 클래스를 통한 상속

`super`키워드를 통해 `Person`에서 정의한 프로퍼티 및 메소드를 모두 받아온다.

```javascript
class Teacher extends Person {
    constructor(subject) {
        super(name, age);
        this.subject = subject;
    }
}
```




