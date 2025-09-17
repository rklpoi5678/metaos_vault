## Mongoose 문법 정리

**데이터베이스  연동하기**
`mongoose.connect()` 함수를 사용해 커넥션을 만들고 사용한다.
연동확인
```js
import mongoose  from 'mongoose';

await dbCounnect();
console.log(mongoose.connection.readyState);
```

**모델 만들기**
`mongoose.Schema()`  를 사용해서 스키마를 생성
`mongoose.model`참조할 수 있기 때문에 잘 지정했는지 반드시 확인
모듈 파일을 import할 때마다 모델을 생성하는 일이 일어나지 않도록 `mongoose.models['ShortLink'] || mongoose.model('ShortLink',shortLinkSchema)`처럼 작성해 둔 부분도 눈여겨 봐 주세요.

```js
import mongoose from 'mongoose';

const shortLinkSchema = new mongoose.Schema(
  {
    title: { type: String, default: '' },
    url: { type: String, default: '' },
    shortUrl: { type: String, default: '' },
  },
  {
    timestamps: true,
  }
);

const ShortLink =
  mongoose.models['ShortLink'] || mongoose.model('ShortLink', shortLinkSchema);

export default ShortLink;

```

## 모델 다루기
생성
```js
const newShortLink = await ShortLink.create({
	title: '코드잇 커뮤니티',
	url: 'https://www.coderit.kr/..'
})
```
여러개 조회
```js
const shortLinks = await ShortLink.find();
const filteredShortLinks = await ShortLink.find({ shortUrl: 'c0d317'})
```
아이디로  하나만 조회
```js
const shortLink = await ShortLink.findById('n3x7j5')
```
아이디로 업데이트하기
```js
const updatedShortLink = await ShortLink.findByIdAndUpdate('n3x7j5'.{...});
```
아이디로 삭제하기
```js
await ShortLink.findByIdAndDelete('n3x8j5');
```

조건으로 하나만 조회
```js
const shortLink =  await ShortLink.findOne({ shortUrl: 'c0ds..'})
```
조건으로 업데이트
```js
await ShortLink.updateOne({_id: 'n3x8j4'}, { ... });

const updatedShortLink = await ShortLink.findOneAndUpdate({_id: 'n3x8j5}, {...});
```
조건으로 삭제하기
```js
await ShortLink.deleteOne({_id: 'n3xj32'},{...})
const deletedShortLink = await ShortLink.findOneAndDelete({_id: 'n3x8j5'}, {...})
```