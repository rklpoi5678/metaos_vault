## 핵심
클라이언트사이드: HTML안 JS가 돌아가고 JS에 리액트가 돌아가는방식이다.
- 초기 로딩이 느리다.
- 검색 엔진에 제공할 수 있는 정보가 적다
이런 단점을  극복하기위해 프리렌더링(Pre-rendering)이라고한다.
미리 html을 저장해서  보여주거나 ,  서버에서 html먼저 보내는것이다.

Next.js 장점
프리렌더링을 대신해줌, Vercel로 서버 호스팅을 쉽게할수있다.
파일 시스템 기반  라우팅(앱라우팅)을 적용하기에 쉽게 라우팅을 할수있다.

## CSS 적용하기
```jsx
import styles from '../styles/Home.module.css';
// global.css: 여거서 쓰면 전역으로 스타일을 넣을수있다.
// @을 쓰면 최상위에서 사용할수있다.
import '@/styles/global.css';

export default function Home() {
	return (
		<h1 className={styles.title}>
			Hello Next.js!	
		</h1>	
	)
}
```

경로에 맞게 페이지를 보내주는것을 라우터라고 한다. 바꿔끼울수있다.

## 파일시스템 기반  라우팅이란?
라우팅: 어떤 주소에 어떤  페이지를 보여줄지 정하는 것이다.
파일시스템 기반 라우팅: 파일의  경로가 주소에  매칭되는 라우팅 방식
> 파일의 경로가 곧 주소가된다.

## 페이지 나누기
폴더명에(파일에) 대괄호를 쓰면 변수명처럼 사용할수있다.
이것을 넥스트에서는 파라미터로 정의한다.
export default로 만들면 페이지가된다.

## Link 컴포넌트
link컴포넌트를 사용하면 필요한부분만 사용하기떄문에, 내부적으로a태그보다 최적화가 되어있다.
일반 a태그는 풀리로드 한다.
```jsx
import Link from 'next/link';
import styles from '@/styles/Home.module.css';

export default function Home() {
  return (
    <div>
      <h1>Codeitmall</h1>
      <ul>
        <li>
          <Link href="/products/1">첫 번째 상품</a>
        </li>
        <li>
          <Link href="/products/2">두 번째 상품</a>
        </li>
        <li>
          <Link href="/products/3">세 번째 상품</a>
        </li>
        <li>
          <Link href="https://codeit.kr">코드잇</a>
        </li>
      </ul>
    </div>
  );
}
```
## useRouter:  쿼리 사용하기
```js
import { useRouter } from 'next/router';

export default function Home()  {
	const router = useRouter();
	const { id } = router.query;  //라우터에서 id라는 값을 가져온다.
	
	return <div>Product {id} 페이지</div>;
}
```
## useRouter: 페이지 이동하기
```js
import { useState } from 'react';
import { useRouter } from 'next/router';

export default function SearchForm({ initialValue = '' }) {
  const router = useRouter();
  const [value, setValue] = useState(initaialValue);

  function handleChange(e) {
    setValue(e.target.value);
  }

  function handleSubmit(e) {
    e.preventDefault();
    
    if(!value) {
		router.push('/'); 
		retrun;
    }
    router.push(`/search?q=${value}`);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input name="q" value={value} onChange={handleChange} />
      <button>검색</button>
    </form>
  );
}

// index.js
<>
	<h1></h1>
	<SearchForm />
	...
// search.js
	<h1></h1>
	<SearchForm initialValue={q} />
	<h2> {q} 검색 쿼리 </h2>

```

## API연동하기
```js
import axios from 'axios';

const instace = axios.create({
	baseUrl: 'https://learn.codeit.kr/api/codeitmall',
});

export default instance;
```
```js
import { useRouter } from 'next/router';
import { useState } from 'react';
import axios from '@/lib/axios';

export default function  Product() {
	const [product, setProduct] = useState();
	const router = useRouter();
	const { id } = router.query
	
	async function getProduct(targetId) {
		const res = await axios.get(`/products/${targetId}`);
		const nextProduct = res.data;
		setProduct(nextProduct);
	}
	
	useEffect(() => {
		if (!id) return;	
		
		getProduct(id);
	}, [id])
	
	if (!product) return null;
	
	return (
		<div>
			<h1>{product.name}</h1>	
			<img
				src={product.imgUrl}
				alt={product.name}
			/>
		</div>	
	); 
}


```