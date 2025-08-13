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
console.log(codeit.get(2017))
```