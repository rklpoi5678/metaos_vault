## 핵심
flex-row:기본값 , 왼쪽에서 오른쪽으로, 가로로 나란히 배치
flex-row-reverse: 오른쪽에서 왼쪽으로, 가로로 뒤집어 배치
- ![[Pasted image 20250714151737.png]]
- flex-col: 위에서 아래로, 세로로 쌓아서 배치
- flex-col-reverse: 아래에서 위로, 세로로 뒤집어배치
	- ![[Pasted image 20250714151827.png]]

### **반응형**
md:,lg: 같은 접두어를 함께 사용하면 화면 크기에 따라 배치 방향을 다르게 할수 있다.
```HTML
<div class="flex flex-col md:flex-row bg-gray-200 p-4">
    <div class="p-2 bg-blue-300">아이템 1</div>
    <div class="p-2 bg-green-300">아이템 2</div>
</div>
```

## 정리
가로 배치, 세로 배치, 그리고 순서를 뒤집을지 결정하는것이다.

