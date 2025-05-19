
## 목표
동남아 현지 길가에 숨어 있는 오프라인 투어사를 지도위에 그려서 여행자에게 '발로 뛰는 정보'를 던져 준다
- 여행사 관점: "구글맵에 안 뜨는 작은 여행사도 한눈에"
- 투어사 관점: 무료 노출->예약 송출-> 수수료 모델로 이어질 잠재 고객 유입
- 사업 관점: 위치 데이터 -> 후기/예약 -> 결제 -> 추천 알고리즘으로 자연스러운 확장

## 기능
| 영역   | 반드시 구현                                                     | 이후 단계 (2~3개월)              |
| ---- | ---------------------------------------------------------- | -------------------------- |
| 지도   | ▸ 현재 위치 기준 반경 3 km 내 투어사 마커▸ 터치 시 간단 카드(이름, 거리, 전화, 현지 가격) | ▸ 거리·테마 필터▸ 오프라인/온라인 예약 버튼 |
| 데이터  | ▸ 사전 크롤/크라우드소싱 CSV → S3/Firestore 저장                       | ▸ 업주 직접 등록 포털▸ 리뷰·사진 업로드   |
| 오프라인 | ▸ 마지막 조회 반경 캐싱(AsyncStorage)                               | ▸ 전체 국가 오프라인 패키지 다운로드      |
| 언어   | ▸ 한국어 · 영어 UI                                              | ▸ 베트남어 · 태국어 · 라오어         |

## 기술
| 레이어       | 선택 이유                                                 | 핵심 패키지                                                                                                                                                                                                                                                                                                                                                                                          |
| --------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **클라이언트** | Expo ▶ 최단시간 빌드·OTA 업데이트 (앱스토어 심사 대기 최소화)              | `expo`, `react-native-maps` (Expo SDK 포함) ([Medium](https://medium.com/geekculture/mapview-in-expo-react-native-5aa69eb81519?utm_source=chatgpt.com "MapView in Expo/React Native - Medium"), [Stack Overflow](https://stackoverflow.com/questions/57598520/react-native-maps-with-expo?utm_source=chatgpt.com "react-native-maps with expo - Stack Overflow")), react-native-google-mobile-ads |
| **상태**    | 무의미한 리덕스 보일러플레이트 제거, 훅 기반 간결함                         | `zustand` (미들웨어: persist + immer) ([Zustand Documentation](https://zustand.docs.pmnd.rs/?utm_source=chatgpt.com "Zustand: Introduction"), [Zustand Documentation](https://zustand.docs.pmnd.rs/integrations/persisting-store-data?utm_source=chatgpt.com "Persisting store data - Zustand"))                                                                                                    |
| **스타일**   | Tailwind 문법으로 빠른 프로토타입·다크모드 대응                        | `nativewind` + `tailwind.config.js` + Babel 플러그인 ([Nativewind](https://nativewind.dev/?utm_source=chatgpt.com "NativeWind: Home"), [DEV Community](https://dev.to/gamertense/getting-started-with-nativewind-using-tailwind-css-in-react-native-13e6?utm_source=chatgpt.com "Getting Started with NativeWind: Using Tailwind CSS in React Native"))                                             |
| **백엔드**   | 초기엔 정적 JSON → 곧 Supabase / Firebase + Cloud Functions | supabase(인증,RAWGEO데이터),Firebase(AdMob,GA사용)                                                                                                                                                                                                                                                                                                                                                     |
| **언어**    | 로컬라이징화 미국어,베트남어,라오어,태국어,일본어                           | i8n과 비슷한 라이브러리                                                                                                                                                                                                                                                                                                                                                                                  |

## 폐업플래그
1. 현지 제보 2건 이상
2. 전화 3회 불통시
3. is_closed = True

## 크롤 및 지도 데이터
오프라인 투어사 위치가 목적이니 tourism=information과 shop=travel_agency위주로 공략
office=travel_agent는 회사나 사무용이어서 취지랑 안맞았음

### 지원
JAVA Heap 사이즈늘리기 Mxm 6g(8기가 바이트에 적당) 코틀린은 2048m(메가바이트)으로 여유분늘리기

expo-admob-ads(기술지원종료 gradle 8버전이상에는 작동안함) 관련 사용금지하고 react-native-google-mobile-ads 사용권장 

AdMob사용시 Firebase도 필요하다. 광고 데이터 추적, 수익 분석하기 위해 FirebaseSDK와 연동해야함 Abmob설정시 Firebase App ID필요 google-services-.json파일을 통해 Firebase프로젝트와 연결 Admob광고 최적화 기능등을 활용 -> 광고 효율성을 높이는 데이터 분석