## 핵심
어떤 그림을 올리고, 어떤 그림을 아래로 깔아야 할까? 나 요소들이 겹칠때 누가 위에, 누가 아래에 보일지 순서를 결정하는것

HTML쓰인 순서대로 나오는 경향이 있어, 나중에 쓰인 코드가 위에 보인다. 중요한 뷰가 위에 제대로 올라오지 않는 문제가 생길 수 있다.

## 용법
z-index의 한가지 전제 조건, 바로 z-index가 적용될 요소는 position 속성 중 static이 아니어야한다!!!
- 일반 바닥에 놓인 static 요소는 번호가 있어도 의미가 없다.(테이블에 놓여져있어야 요소 겹침 순서를 넣을수있다.)

테일윈드는 0~50 (step10) 단위로 그리고 9999처럼 큰 숫자까지 다양한 z-index클래스 사용한다.
- z-0: z-index-0;
- z-10, z-20, ..., z-50: 숫자가 클수록 더 위에 보인다.
- z-auto: 브라우저가 자동으로 결정
- z-\[-10](음수): 다른 요소들 아래로 가라앉게 만들 때 사용한다.
```HTML
<div class="relative h-48 w-48 bg-gray-200"> <div class="absolute inset-0 bg-blue-500 opacity-75">
        </div>

    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 bg-red-500 w-24 h-24 z-10">
        </div>

    <div class="absolute top-0 right-0 bg-green-500 w-16 h-16 z-20">
        </div>

</div>
```
1. bg-blue-500 박스가 가장 아래
2. bg-red-500 박스 (z-10)가 파란 박스 위에 보임
3. bg-green-50 박스 (z-20)가 빨간 박스 위에보여, 모든 요소 중 가장 위에 나타남
