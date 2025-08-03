# 핵심

객체에 !== undefined 를 사용하여 해당 객체가 undefined 인지 확인이 가능하며

```plaintext
 in으로 'name' in codeit 처럼 해당 오브젝트가 있는지 확인이 가능합니다.
```

@03:09

### in을 사용하는이유

코드가 더 간결해지기도 하고

실수를 방지할수있기에 사용한다.

(객체의 밸류값으로 undefined가 들어있는데 codeit.name !== undefined를 사용하면 false가 나오는 위험성존재)