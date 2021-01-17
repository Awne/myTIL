

## Object

### Object.assign

메소드를 가지고있는 객체가 존재함.
```javascript
const healthObj = {
    showHealth : function() {
        console.log("운동시간 : " + this.healthTime)
    }
}
```

아래 코드는 `Object.create`를 통해 부모를 모셔온 새 객체를 만든 뒤 프로퍼티를 추가함.
```javascript
const myHealth = Object.create(healthObj);

myHealth.healthTime = "11:00";
myHealth.name = "crong";
```

아래 코드는 위 코드와 결과는 같지만 `Object.assign`을 통해 프로퍼티를 한번에 추가할 수 있음.
```javascript
const myHealth = Object.assign(Object.create(healthObj), {
    name : "crong",
    healthTime : "11:22"
})
```
1. 첫 인자는 어디에 합칠지 설정
2. 아무것도 상속받지 않는 객체에 추가하려면 첫 인자를 `{}`로 설정.
3. 두번째 인자부터는 합칠 객체들을 설정
4. 합칠 객체들 사이에 중복된 키가 있다면 덮어쓰기를 통해 우측 요소가 적용.

### Object.setPrototypeOf

`Object.create`처럼 프로토타입을 정해줄 수 있다. 반환값은 새로운 객체.

```javascript
Object.setPrototypeOf(Bird, Animal)
```

`Bird`의 프로토타입을 `Animal`로 설정함.









### 객체

아래 코드는 `Awne 27`을 출력한다.

변수 `name`은 `obj.name`을, `age`는 `obj.age`를 할당받는다.
```javascript
let obj = {
    name : "Awne",
    from : "Korea",
    age : 27,
}

let {name, age} = obj;
console.log(name, age);
```

변수의 이름을 바꿀 수도 있다.

아래 코드는 `name` `age` 대신 `myName` `myAge` 를 사용한다.
```javascript
let {name : myName, age : myAge} = obj;
console.log(myName, myAge);
```





### JSON 파싱

JSON 데이터를 파싱하는데도 유용하게 사용할 수 있다.

아래와 같은 데이터가 있다고 가정한다.
```javascript
let stockmarket = [
    {
        title : "KOSPI",
        nation : "Korea",
        companies : [
            "Samsung electronics", "SK Hynix", "Hyundai car"
        ],
    },
    {
        title : "NASDAQ",
        nation : "USA",
        companies : [
            "Microsoft", "Amazon", "Alphabet"
        ],
    }
]
```

아래 코드는 변수`nas`에 `stockmarket[1]`을 할당한다.
```javascript
let [,nas] = stockmarket;
```

아래 코드는 `NASDAQ [ 'Microsoft', 'Amazon', 'Alphabet' ]`을 출력한다.
```javascript
let {title, companies} = nas;
console.log(title, companies);
```

아래 코드는 위 코드와 동일하게 동작한다.
```javascript
let [, {title : 이름, companies : 기업}] = stockmarket;
console.log(이름, 기업);
```



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