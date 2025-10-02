## README 개요
node.js을 위한 강력하고 성능 중심의 모든 기능을 갖춘 Redis클라이언트
Redis >= 26.12 Redis 7.x와 완벽하게 호환됨
node-redis가 권장되는 클라이언트 라이브러리

해시필드만료, 향후 명령, Redis Stack및 Redis8 에 사용할수있는 기능(검색,JSON,시계열, 확률적 데이터 구조)를 지원

## 기능
0. 모든 기능을 갖춤 (Cluster,Sentinel, Streams,Piplining 및 루아 스크립팅, Redis Functions, Pub/Sub(바이너리 메시지 지원))을 지원한다.
1. High performance 고성능
2. Delightful API. It works with Node callbacks and Native promises. 야 즐겁다 API
3. 여령 인수 및 응답의 반환
4. 투명한 키 접두사
5. 루아 스크립팅을 위한 추사오하를 통해 사용자 정의 명령을 정의
6. 이진 데이터를 지원
7. TLS 지원
8. 오프라인 대기열 및 준비 확인을 지원
9. Map 및 Set과 같은 ES6 유형을 지원
10. GEO 명령
11. Redis ACL지원
12. 정교한 오류 처리 전략
13. NAT 매핑 지원
14. 자체 파이프라인 지원
15. 100% TypeScript로 작성되었으며 공식 선언이 제공됩니다.

## 빠른시작
> npm install ioredis
> npm install --save-dev @types/node

## BASIC USAGE
```js
// ioredis를 가져옵니다.
// TypeScript 프로젝트인 경우 `import { Redis } from "ioredis"`를 사용할 수도 있습니다.
// 참고: `import Redis from "ioredis"`는 여전히 지원되지만, 다음 주요 버전에서 더 이상 사용되지 않을 것입니다.
const Redis = require("ioredis");

// Redis 인스턴스를 생성합니다.
// 기본적으로 localhost:6379에 연결됩니다.
// 곧 연결 옵션을 지정하는 방법을 다룰 예정입니다.
const redis = new Redis();

redis.set("mykey", "value"); // 명령이 성공하면 "OK"로 해결되는 Promise를 반환합니다.

// ioredis는 node.js의 콜백 스타일을 지원합니다.
redis.get("mykey", (err, result) => {
  if (err) {
    console.error(err);
  } else {
    console.log(result); // "value"를 출력합니다.
  }
});

// 또는 마지막 인수가 함수가 아니면 ioredis는 Promise를 반환합니다.
redis.get("mykey").then((result) => {
  console.log(result); // "value"를 출력합니다.
});

redis.zadd("sortedSet", 1, "one", 2, "dos", 4, "quatro", 3, "three");
redis.zrange("sortedSet", 0, 2, "WITHSCORES").then((elements) => {
  // `redis> ZRANGE sortedSet 0 2 WITHSCORES` 명령을 실행했을 때와 같이 ["one", "1", "dos", "2", "three", "3"]이 반환됩니다.
  console.log(elements);
});

// 모든 인수는 Redis 서버에 직접 전달되므로,
// 기술적으로 ioredis는 모든 Redis 명령을 지원합니다.
// 형식은 `redis[SOME_REDIS_COMMAND_IN_LOWERCASE](ARGUMENTS_ARE_JOINED_INTO_COMMAND_STRING)`입니다.
// 따라서 아래 구문은 CLI의 `redis> SET mykey hello EX 10`과 동일합니다.
redis.set("mykey", "hello", "EX", 10);
```

더 많은 예제는 examples/폴더를 참조하십시오
- [TTLTTL](https://github.com/redis/ioredis/blob/main/examples/ttl.js)
- [Strings문자열](https://github.com/redis/ioredis/blob/main/examples/string.js)
- [Hashes해시](https://github.com/redis/ioredis/blob/main/examples/hash.js)
- [Lists목록](https://github.com/redis/ioredis/blob/main/examples/list.js)
- [Sets설정](https://github.com/redis/ioredis/blob/main/examples/set.js)
- [Sorted Sets정렬된 세트](https://github.com/redis/ioredis/blob/main/examples/zset.js)
- [Streams스트림](https://github.com/redis/ioredis/blob/main/examples/stream.js)
- [Redis Modules](https://github.com/redis/ioredis/blob/main/examples/module.js) e.g. RedisJSONRedis 모듈 (예 : RedisJSON
- 모든 레디스 명령이 지원된다.

## Redis에 연결
새 레디스 인스턴스가 생성되면
레드스에 대한 연결이 동시에 생성된다.
다음을 통해 연결할 레디스를 지정할수있다.
```js
new Redis(); //localhost (127.0.0.1:6379)
new Redis(6380) //localhost:6380 (...:6380)
new Redis(6379, "192.168.1.1")
new Redis("/tmp/redis.sock")
new Redis({
	port: 6379, // Redis port
	host: "127.0.0.1", //Redis host
	username: "default", // needs Redis >= 6
	password: "my-tcp-secret",
	db: 0 // Defaults to 0
});
```
TLS 암호화를 사용할 때 연결 옵션을 redis://URL or rediss://URL 로 지정가능
```js
// Connect to 127.0.0.1:6380, db 4, using password "authpassword":
new Redis("redis://:authpassword@127.0.0.1:6380/4");

// Username can also be passed via URI.
new Redis("redis://username:authpassword@127.0.0.1:6380/4");
```

## 펍/구독
게시.구독 패턴을 구현할수있는 몇가지 명령을 제공한다.
게시자와 구독자의 두 가지 패턴
ioredis는 Node.js의 내장 이벤트 모듈을 활용하여 pub/sub을 매우 쉽게 사용할 수 있도록 한다. 하낳는 채널에 메시지를 게시하는 publisher.js이고 다른 하나는 특정 채널의 메시지를 수신하는 subscriber.js이다.
```js
// publichsre.js
import { Redis } from "ioredis";

const redis = new Redis();

setInterval(() => {
	const message = { foo: Math.random() };
	// my-channel-1 or my-channel-2 randomly
	const channel = `my-channel-${1 + Math.round(Math.random())}`;

	// 메시지는 문자열 또는 버퍼일 수 있다.
	redis.publish(channel, JSON.stringify(message));
	console.log("Published %s to %s", message, channel);
}, 1000)
```
```js
// subscriber.js
import { Redis } from "ioredis";

const redis = new Redis();

redis.subscribe("my-channel-1", "my-channel-2", (err, count) => {
	if (err) {
	// 다른 명령과 마찬가지로 subscribe()는 몇 가지 이유로 실패할 수 있습니다.
   // ex 네트워크 문제.
		console.error("Failed to subscribe: s%", err.message);	
	} else {
	// 'count'는 이 클라이언트가 현재 구독하고 있는 채널 수를 나타냅니다.
		console.log(
	      `Subscribed successfully! This client is currently subscribed to ${count} channels.`
		);
	}
});

redis.on("message", (channel, message) => {
	console.log(`Received ${message} from ${channel}`);
});
	// 'messageBuffer'라는 이벤트도 있는데, 이는 'message'와 동일합니다.
	// 문자열 대신 버퍼를 반환합니다.
	// 메시지가 이진 데이터일 때 유용합니다.
redis.on("messageBuffer", (channel, message) => {
	console.log(channel, message);
})
```
동시에 두가지 역할을 할수없다. sub/pub을 실행하면 "구독자" 모드로 들어간다. 이 시점부터 구독 세트를 수정하는 명령만 유효하다
동일한 파일/프로세스에서 pub/sub을 수행하려면 별도의 연결을 만들어야 한다.
```js
const Redis = require("ioredis");
const sub = new Redis();
const pub = new Redis();

sub.subscribe(/* ... */); // From now, `sub` enters the subscriber mode.
sub.on("message" /* ... */);

setInterval(() => {
  // `pub` can be used to publish messages, or send other regular commands (e.g. `hgetall`)
  // because it's not in the subscriber mode.
  pub.publish(/* ... */);
}, 1000);
```

PSUBSCRIBE는 이름이 패턴과 일치하는 모든 채널을 구독하려는 경우에도 유사한 방식으로 지원한다.
```js
redis.psubscribe("pat?ern", (err, count) => {});

// Event names are "pmessage"/"pmessageBuffer" instead of "message/messageBuffer".
redis.on("pmessage", (pattern, channel, message) => {});
redis.on("pmessageBuffer", (pattern, channel, message) => {});
```

