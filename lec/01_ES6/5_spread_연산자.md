# spread 연산자

전개연산자라고도 불리는데 ... 를 이용해서 표현하는 연산자입니다.

spread 연산자는 다양항 상황에서 자주 사용되는 주요 문법인데, 각각의 경우를 하나씩 살펴보도록 하겠습니다.

## 배열

### 깊은복사

아래는 arr1 배열 변수를 arr2에 할당하고, 두 변수의 같음을 확인하는 코드입니다.

```js
const arr1 = [10, 20, 30];
const arr2 = arr1;

console.log(arr1 === arr2); // true
```

배열은 참조 자료형이고 별도의 주소값을 가지고 있기 때문에 arr1이 가지고 있는 배열의 주소값을 arr2도 가지게 됨으로 위 코드의 arr1, arr2는 같습니다.

그래서 하나만 변경해도 자신이 바라보고 있는 배열의 주소 위치가 같기 때문에 같이 변합니다.

```js
const arr1 = [10, 20, 30];
const arr2 = arr1;

arr1.push(40); // 배열에 40추가

console.log(arr1); // [10, 20, 30, 40]
console.log(arr2); // [10, 20, 30, 40]
```

이렇게 하나의 데이터가 변경될 때 다른 쪽의 데이터도 변경되는 복사를 얕은 복사라고 합니다.

깊은 복사를 하고 싶다면 spread 연산을 이용하면 됩니다.

```js
const arr1 = [10, 20];
const arr2 = [...arr1];

arr1.push(30);

console.log(arr1); // [10, 20, 30]
console.log(arr2); // [10, 20]
```

arr2에 arr1의 배열이 전개되어서 새로운(new) 배열로 다시 탄생하기 때문에 arr2는 arr1의 배열 변수의 주소값을 가지고 있지 않습니다. 따라서 arr1의 값을 변경해도 arr2는 영향을 받지 않습니다. 이를 깊은 복사라고 합니다.

### 병합

두 배열을 합치려면 보통 아래처럼 사용합니다.

```js
const arr1 = [10, 20];
const arr2 = [30, 40];

const combined1 = [arr1[0], arr1[1], arr2[0], arr2[1]];
//또는
const combined2 = arr1.concat(arr2);
```

하지만 spread 연산자를 사용하면 아래처럼 간단히 가능합니다.

```js
const arr1 = [10, 20];
const arr2 = [30, 40];
const combined = [...arr1, ...arr2];
```

### 순서 변경하기

```js
const arr1 = [10, 20];
const arr2 = [30, 40];
const combined = [...arr2, ...arr1];
```

## 객체

### 깊은 복사

객체에서도 깊은 복사 용도로 사용할 수 있습니다.

```js
const obj1 = {name: '철수'};
const obj2 = obj1;

obj1.age = 20;

console.log(obj1); // { name: '철수', age: 20 }
console.log(obj2); // { name: '철수', age: 20 }
```

```js
const obj1 = {name: '철수'};
const obj2 = {...obj1};

obj1.age = 20;

console.log(obj1); // { name: '철수', age: 20 }
console.log(obj2); // { name: '철수' }
```

### 병합

병합도 배열과 비슷하지만 조금 다른점이 있습니다.

```js
const obj1 = {name: '철수'};
const obj2 = {age: 20};
const combinedObj = {...obj1, ...obj2}; // {name : '철수', age: 20}

const newObj = {...obj1, age: 50}; // {name:'철수', age:50}
```

배열과 조금 다른 점은 키(key)가 중복이 되면 마지막 키가 덮어씌여진다는 점입니다.

```js
const obj1 = {
	name: '철수',
	age: 20,
};

const obj2 = {
	name: '영희',
	age: 30,
};

const combinedObj = {...obj1, ...obj2}; // {name:"영희", age:30}
```

## 함수

### 가변인자

```js
function add(...args) {
	return args.reduce((accumulator, currentValue) => accumulator + currentValue);
}

console.log(add(10, 20, 30, 40)); // 100
```
