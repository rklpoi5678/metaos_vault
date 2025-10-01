## 타입스크립트 적용하기 정리
패키지 설치: @types, npm사이트 찾기, 타입스크립트를 지원해준다면 따로 설치할필요가없다.
## Express 핸들러 타입
Request,Response,NextFunction
RequestHandler

## 타입 커스텀
 외부 모듈에 대해 declare문법을 활용하면 타입을 덮어쓸수있음, interface 문법의 경우 이미 정의된 interface와 합쳐지기 때문에 내가 원하는 특정  프로퍼티는 아래와 같이 간단히 추가해볼수있다.
 ```ts
 // express.d.ts
 import Express from  'express';
 
 declare global {
	namespace Express {
		interface Request {
			valid?: boolean;	
		}	
	} 
 }
 ```
## ORM에서 타입 사용하기

**몽구스**
@types/mongoose 패키지 설치, 스키마를 정의할때 직접  인터페이스를 정의, 이걸 제네릭  문법으로 활용하게된다.
```ts
import { Schema, model, connect } from 'mongoose';

// 1. Create an interface representing a document in MongoDB.
interface IUser {
  name: string;
  email: string;
  avatar?: string;
}

// 2. Create a Schema corresponding to the document interface.
const userSchema = new Schema<IUser>({
  name: { type: String, required: true },
  email: { type: String, required: true },
  avatar: String
});

// 3. Create a Model.
const User = model<IUser>('User', userSchema);

/**
* 또 한 가지 특이한 점은 MongoDB에서는 데이터베이스에서 알아서 만들어 주는
* 아이디가 있는데요. 이런 아이디에 대해서는 반드시 `Types.ObjectId` 타입을 써야 한다고 * 하네요.
*/
import { Schema, Types } from 'mongoose';

// 1. Create an interface representing a document in MongoDB.
interface IUser {
  name: string;
  email: string;
  // Use `Types.ObjectId` in document interface...
  organization: Types.ObjectId;
}
```

## Prisma
자체적으로 타입스크립트를 지원한다.
더 나아가 필요한 타입 정의까지도 알아서 만들어준다.
```schema.prisma
datasource db {
  provider = "mongodb"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model File {
  id        String   @id @default(auto()) @map("_id") @db.ObjectId
  name      String
  path      String
  size      Int
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```
```ts
// 아래와 같은 코드가 자동으로 추론이 된다. File이라는  타입을 알아서 만들어주고, 그안에 neme,path,size등등의  프로퍼티의 타입이 정의되는 것이다.
const file = await prisma.file.create({
  data: {
    ...req.body,
    path: req.file?.path.replace(/^public\//, 'http://localhost:3000/'),
    size: req.file?.size,
  },
});
```
```ts
// @prisma/client에서 타입을 가져와서 사용하면 된다.
import { File } from  "@prisma/client"
import  prisma from  "../prisma"

export  default async function createPost (
	title: string,
	content: string,
		file?: File // File타입
) {
	// ...
}
```