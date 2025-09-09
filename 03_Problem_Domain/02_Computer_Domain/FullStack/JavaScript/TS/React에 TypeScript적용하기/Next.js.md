## Pages Router타입
커스텀 app
```app.tsx
AppProps라는 타입을 next/app패키지에서 불러와서 아래처럼사용
import { AppProps } from 'next/app'

export default function App ({ Component, pageProps }: AppProps) {
	// ....
}
```

## 프리렌더링
빌드  시점에 리엑트 코드를 미리 렌더링해 둘수있다. 이런 것을 정적생성(Static  Generation)

## 서버사이드 렌더링
서버에 리퀘스트가 들어올 때마다 렌더링해서 보내주는 서버사이드 렌더링의 경우에도 비슷한 방식으로 해주면 된다.
```jsx
import Image from 'next/image';

export async function getServerSideProps(context) {
  const productId = context.params['id'];

  let product;
  try {
    const res = await fetch(`https://learn.codeit.kr/api/codeitmall/products/${productId}`);
    const data = await res.json();
    product = data;
  } catch {
    return {
      notFound: true,
    };
  }

  return {
    props: {
      product,
    },
  };
}

export default function ProductPage({ product }) {
  return (
    <div>
      <h1>{product.name}</h1>
      <Image
        src={product.imgUrl}
        width="480"
        height="480"
        alt={product.name}
      />
    </div>
  );
}

```
수정
```tsx
interface Props {
	product: Product;
}

export const getServerSideProps: getServersideProps<Props> = async (context) => {
	// ...
	return (
		props: {
			product,	
		},
	);
};

export default function ProductPage({ product }: Props)
```

## API라우트
라우트의 타입을 살펴보면 아래와 같이 리퀘스트와, 리스폰스 타입을 지정하면된다.
```tsx
import type { NextApiRequest, NextApiResponse } from 'next';

export default function handler(req: NextApiRequest, res: NextApiResponse) {

}
```
