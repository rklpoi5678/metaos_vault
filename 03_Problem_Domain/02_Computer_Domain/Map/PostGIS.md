
## 오프라인 패키징에서 PostGIS 역할
인터넷 연결 없이도 지도 데이터를 사용할 수 있도록 미리 데이터를 준비하는 과정이다.
PostGIS는 이 과정에서 지도 데이터를 효율적으로 저장하고, 필요한 부분만 추출해서 패키징하는 역할을 한다

## 비유
PostGIS = 지도 데이터를 저장하고 검색할 수 있는 책장
오프라인 패키징 = 필요한 지도 데이터를 미리 정리해서 휴대용 지도책으로 만드는 과정

## 패키징
1. PostGIS를 이용해 투어사 위치 데이터 저장
	1. 각 투어사 위도/경도 정보를 PostGIS 테이블에 저장
	2. 추가적으로 전화번호, 리뷰, 가격 정보도 함께 저장 가능
2. 필요한 지역만 선택해서 오프라인 패키징
	1. 하노이 지역의 투어사만 가져와 -> 쿼리
	2. SELECT * FROM tours WHERE ST_Contains(hanoi_boundary, location);
	3. 이렇게 하면 하노이 지역 안에 있는 투어사만 선택할 수 있음
3.  데이터를 SQLite 또는 MBTiles 형식으로 변환
	1. 오프라인에서 사용할 수 있도록 데이터를 압축하고 저장
	2. ogr2ogr -f SQLite tours.mbtiles tours.geojson
	3. 이렇게 하면 모바일 앱에서 빠르게 로드할 수 있는 오프라인 지도 데이터 생성

### ogr2ogr (=PostGIS에 넣기 위한 명령줄)
GDAL(Geospatial Data Abstraction Libary)에 포함된 명령줄 도구이다.
다양한 지도 데이터 형식 (shapefile,GeoJSON,CSV등) 데이터를 변환하고 가져오거나 내보내는 역할을 한다.

즉, ogr2ogr라는 공장 기계에 넣으면, 그 기계가 자동으로 데이터를 다음어 PostGIS라는 특별한 서랍장에 딱 맞게 정리해주는 것과 같다.
