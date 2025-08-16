## 핵심
sort: 배열을 정렬, 메소드에 아규먼트도 전달되지 않을때 기본적으로 유니코드에 정의된 문자열 순서에 따라 정렬된다.
```js
const letters = ['D', 'C', 'E', 'B', 'A'];
const numbers = [1, 10, 4, 21, 36000];

letters.sort();
numbers.sort();

console.log(letters); // (5) ["A", "B", "C", "D", "E"]
console.log(numbers); // (5) [1, 10, 21, 36000, 4]
// sort시켜 정렬이된모습

/** sort로 내림차순 오름차순 정렬법 */
const number = [1,10,4,21,36000];

// 오름차순
number.sort((a,b) => a - b);
console.log(number); // [1,4,10,21,36000];

// 내림차순
number.sort((a,b) => b - a);
console.log(number); // [36000, 21, 10, 4, 1]

// 한가지 주의점 **메소드를 실행하는 원본 배열의 요소들을 정렬**한다는 점
// 즉, 한번 정렬후 정렬하기 전 순서로 되돌릴 수 없다. -> 미리 다른 변수에 복사하는방법
```

## 여기서 말하는 뺼셈 연산
sort콜백은 "비교하는 방법"을 알려주는 함수다.

반환값 < 0 : a가 b보다 앞에 있어야 한다.
반환값 = 0 : a와 b의 순서를 바꾸지 않는다.
반환값 > 0 : b가 a보다 앞에 있어야 한다.

>"a와 b 두개를 비교했을때 어떤게 먼저 와야하는가를 정하는것"

## reverse 메소드
말그대로 배열의 순서를 뒤집어준다.
sort와 마찬가지로 원본 배열의 요소들을 뒤집어 버린다는점
```js
const letters = ['a','c','b'];
const numbers = [421, 721, 353];

letters.reverse();
numbers.reverse();

console.log(letters); //["b","c","a"]
console.log(numbers); //[353,721,421]
```

## Map
이름이 있는 데이터를 저장한다는점에서 객체와 비슷하다.
점표기법이나 대괄호 표기법으로 접근하는 일반 객체와 다르게 map은 메소드를 통해서 값을 추가하거나 접근할 수 있다.|

- map.set(key,value): key를 이용해 value를 추가하는 메소드
- map.get(key): key에 해당하는 값을 얻는 메소드. key가 존재하지 않으면 undefined를 반환
- map.has(key): key가 존재하면 트루, 존재하지 않으면 거짓 를 반환하는 메소드
- map.delete(key): key에 해당하는 값을 삭제 하는 메소드
- map.clear(): Map안의 모든 요소를 제거하는 메소드
- map.size: 요소의 개수를 반환하는 프로퍼티. (메소드가 아닌 점 주의! 배열의 length 프로퍼티와 같은 역활을 한다.)

```js
// Map 생성
const codeit = new Map();

// set 메소드
codeit.set('title','문자열 key');
codeit.set(2017 ,'숫자형 key');
codeit.set(true ,'불린형 key');

// get 메소드
console.log(codeit.get(2017)); //숫자형 key
console.log(codeit.get(true)); //불린형 key
console.log(codeit.get('title')); //문자열 key

// has 메소드
console.log(codeit.has('title')); // true

// delete 메소드
codeit.delete(true);
console.log(codeit.get(true)); // undefined
console.log(codeit.size); // 2

// clear 메소드
codeit.clear();
console.log(codeit.get(2017)); // undefined
console.log(codeit.size); // 0
```
Map객체는 메소드를 통해 값을 다루기에, 다양한 자료형을 키로 활용할 수 있다는 장점이 있다.

## Set
여러 개의 값을 순서대로 저장한다는 점에서 배열과 비슷하다.
맵과 똑같이 new로 객체를 생성하고 아래와 같은 메소드를 통해 Set안의 여러 값들을 다룰 수 있다.
- set.add(value): 값을 추가하는 메서드 (메소드를 호출한 자리에는 추가된 값을 가진 Set 자신을 반환)
- set.has(value): Set 안에 값이 존재하면 true, 아니면 false를 반환하는 메소드
- set.delete(value): 값을 제거하는 메소드. (메소드를 호출한 자리에는 셋 내에 값이 있어서 제거에 성공하면 트루, 아니면 거짓을 반환)
- set.clear(): Set 안의 모든 요소를 제거하는 메소드.
- set size: 요소의 개수를 반환하는 프로퍼티. (메소드가 아닌 이것또한 점이며 배열의 length 프로퍼티와 같은 역할)

```js
// Set 생성
const members = new Set();

// add 메소드
members.add('영훈'); // Set(1) {"영훈"}
members.add('윤수'); // Set(2) {"",""}
members.add('동욱'); // Set(3) {"","",""}
members.add('태호'); // Set(4) {"","",""}

// has 메소드
console.log(members.has('동욱')); // true
console.log(members.has('현승')); // false

// delete 메소드
members.delete('종훈'); // false
consol.log(members.size); // 4
members.delete('태호'); // true
console.log(members.size); // 3

// clear 메소드
members.clear();
conosle.log(members.size); // 0
```
Map은 get메소드로, 그리고 배열은 index를 통해서 개별 값에 접근할수있는데
특이하게 Set에는 개별 값에 바로 접근하는 방법이없다.
```js
// Set 생성
const members = new Set();

// add 메소드
members.add('영훈'); // Set(1) {"영훈"}
members.add('윤수'); // Set(2) {"영훈", "윤수"}
members.add('동욱'); // Set(3) {"영훈", "윤수", "동욱"}
members.add('태호'); // Set(4) {"영훈", "윤수", "동욱", "태호"}

for (const member of members) {
  console.log(member); // 영훈, 윤수, 동욱, 태호가 순서대로 한 줄 씩 콘솔에 출력됨.
}
```
**당연히  Set이라는 이름을 가졌으면 중복을 허용하지 않는 값을 모를때**유용하다.
```js
// Set 생성
const members = new Set();

// add 메소드
members.add('영훈'); // Set(1) {"영훈"}
members.add('윤수'); // Set(2) {"영훈", "윤수"}
members.add('영훈'); // Set(2) {"영훈", "윤수"}
members.add('영훈'); // Set(2) {"영훈", "윤수"}
members.add('동욱'); // Set(3) {"영훈", "윤수", "동욱"}
members.add('동욱'); // Set(3) {"영훈", "윤수", "동욱"}
members.add('동욱'); // Set(3) {"영훈", "윤수", "동욱"}
members.add('태호'); // Set(4) {"영훈", "윤수", "동욱", "태호"}
members.add('동욱'); // Set(4) {"영훈", "윤수", "동욱", "태호"}
members.add('태호'); // Set(4) {"영훈", "윤수", "동욱", "태호"}
members.add('태호'); // Set(4) {"영훈", "윤수", "동욱", "태호"}
```
나중에 중복된 값을 추가하려고 하면 그 값은 무시하는 특징이 있다.
집합이라고 보면된다.
```js
const numbers = [1,3,4,3,3,3,2,1,1,1,5,5,3,2,1,4];
const uniqNumbers = new Set(numbers);

console.log(numbers); // Set(5) {1,3,4,2,5}
```