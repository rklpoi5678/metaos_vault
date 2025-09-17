## 모델 만들기
데이터를 담을 틀이고(모델), 부어서 데이터를 만든다.
```js
// models/ ShortLink.js
import moongose from 'mongoose';

const shortLinkSchema = new mongoose.Schema(
	{
		title: {type: String, default: ''},
		url: {type: String, default: ''},
		shortUrl: {type: String, default: ''},
	}, {
		timestamps: true,	
	}
);

const ShortLink =
	moongose.models['shortLink'] || mongoose.model('shortLink', shortLinkSchema)

export default ShortLink;
```

## 도큐먼트 생성, 조회하기
```js
case 'POST':
	const newShortLink = await ShortLink.create(req.body);
	res.status(201).send(newShortLink);
	break;
```

```js
//[id].js
import dbConnect from 'mongoose';
import ShortLink from  '@/db/models/ShortLink'

export default handler(req,res) {
	await dbConnect() // 먼저 몽구스 디비연결
	const { id } = req.query;	

	...
	case 'GET':
	const shortLink	= await ShortLink.findById(id); //특정 아이디값에 db데이터를 가져옴
	res.send(shortLink);
	break;
}
```
```js

```
