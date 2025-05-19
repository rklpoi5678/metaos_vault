## 핵심(= 지도책)
웹 상에서 편집하고 관리되는 공간데이터베이스 배경지도로 축척 레벨별로 보기 좋게 스타일링된 TMS로서 OSM의 일부 지도 서비스라고 볼수있다.

## 비유
OSM은 전 세계 사람들이 함께 만드는 거대한 지도책이다.
사람들이 함께 모여서 각자의 지역을 지도에 추가하는것이다.
이런 방식으로 만들어진 **오픈소스 지도 데이터베이스**이다.

---
## Overpass API (지도책에서의 검색 도구)
OSM에 요청하여 원하는 공간 객체를 받을 수 있는 API가 Overpass API이다.
OSM은 node,way등의 구조 내에 다양한 태그(Tag)로 분류되어있다.

## 비유
OSM에서 필요한 정보만 뽑아오는 검색 도구이다.
예를들어 서울에 있는 모든 공원 같은 특정 정보를 찾고 싶다면 바로 OverpassAPI를 사용하여 OSM 데이터베이스에서 특정 조건에 맞는 정보를 빠르게 검색할 수 있도록 도와주는 도구이다.
- 5KM 반경 안에 있는 모든 카페
- 이 도시에 있는 모든 병원
- 특정 도로의 좌표 정보

## Overpass-turbo
쿼리문을 테스트해볼 수 있는 서비스이다.
쿼리문 입력 창에 지역명 및 주차장 태그 (amenity 하위의 parking)로 쿼리문을 작성하고 , Run 버튼을 누르면 오른쪽의 지도 상에서 주차장의 위치와 속성정보를 확인할수있다.

### 라이선스는?
Overpass API (AGPL v3), overpass-turbo (MIT), OSM 원본 데이터 (ODbL 1.0)

|항목|라이선스|비고|
|---|---|---|
|**OSM 원본 데이터**|**ODbL 1.0**|지도·POI를 표시할 때 “© OpenStreetMap contributors” 필요|
|**타일(예: carto tiles)**|타일 서버별 약관|대부분 “OSM attribution” 필요, 상업적 사용 시 추가 제약 가능|
|**내 쿼리 스크립트**|내가 결정|Overpass 쿼리 자체는 저작권 창작물로 보기 어렵지만, 길고 복잡한 스크립트라면 라이선스를 명시 가능|
### 테스트 레시피
# 베트남 전국 관광사 좌표 GeoJSON 예시
```bash
curl -o vietnam_tour_agencies.json \
  "https://overpass-api.de/api/interpreter?data=[out:json];
   area['name'='Vietnam']->.a;
   node(area.a)['tourism'='agency'];
   out center;"
```
- lat,lon(위도,경도) + name 태그확보
--> 초기 씨앗 데이터 확보
- 같은 쿼리에서 국가 코드를 바꿔 라오스.태국 데이터를 한번에 생성한다
#### 2-B Google Places “스팟 증식”


```bash
GET https://maps.googleapis.com/maps/api/place/nearbysearch/json?      location=21.0245,105.8412&radius=40000      &type=travel_agency&key=$API_KEY
```
- 하루 200 쿼리 무료, 응답 안에 `place_id` → `GET /details` 로 전화·웹사이트 추출.
- 40 km 그리드로 동남아 주요 도시를 훑어 빈 구역 보강.

#### 2-C 협회·관청 CSV → 좌표 보강

```typescript
// 예: TTAA 테이블 크롤 → 구글 Geocoding 
rows.forEach(async (r) => {   const { data } = await axios.get("https://maps.googleapis.com/maps/api/geocode/json", {     params: { address: `${r.address}, Thailand`, key: API_KEY }   });   save({ ...r, lat: data.result.lat, lng: data.result.lng }); });
```
- 법적 라이선스 유무 필터링 → “Verified” 뱃지로 표기.

### OSM을 이용하여 서비스를 만든 사례
1. Mapbox: OSM데이터를 기반으로 커스터마이즈가 가능한 지도 시각화로 내비게이션 서비스를 제공하는 프랫폼, Mapbox는 OSM의 풍부한 데이터를 활용하여 사용자에게 직관적이고 미려한 지도 경험을 선사합니다.
2. OSRM(Open Soure Routing Machine): OSM데이터를 이용한 오픈 소스 경로 탐색 엔진이다. 최적의 경로를 실시간으로 계산해 주며, 물류/배송서비스 등에 널리 응용되고 있다. 유연한 경로 제공 서비스를 구축할수있다.
3. OSMnx: 파이썬 기반 라이브러리, OSM데이터를 활용, 거리 네트워크나 인프라 구조를 추출하고 분석하는 데 특화됨, 연구 및 실제 서비스의 의사결정에 중요한 역할을 하며, 학계와 산업 현장에서 활발하게 상용됨
4. 맞춤형 지도 및 위치 기반 서비스: 대중교통 정보, 자전거 경로 안내, 재난 및 긴급상황 모니터링 등 다양한 분야에서 OSM데이터를 기반으로 한 서비스가 제공된다.