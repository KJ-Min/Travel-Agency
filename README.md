# 요약+md vs md 데이터 형식에 따른 성능 비교 (2024년 12월 30일)
[LangSmith Trace 보기 (md 형식 데이터만 사용)](https://smith.langchain.com/public/26e88437-2bd1-4180-8871-ea5c06288e1e/r)  

## 요약 + .md 형식 데이터
- `RAG_TEST_with_summary.csv`
  ```
  29665,"요약: 한일돈까스는 부산광역시 사상구 백양대로에 위치한 경양식 일반음식점입니다. 영업시간은 매일 08:00부터 20:00까지이며, 네이버 평점은 4.4입니다. 편의 시설은 제공되지 않습니다.

  # 한일돈까스

  ## 기본 정보
  - 위치: 부산광역시 사상구 백양대로 949-7
  - 업종: 경양식
  - 영업허가: 일반음식점
  - 지역: 부산광역시 사상구

  ## 상세 설명
  ""한일돈까스""를 부산광역시 사상구의 가 볼 만한 식당으로 추천합니다!

  ## 운영 정보
  - 영업시간: 매일 08:00~20:00
  - 네이버 평점: 4.4000001

  ## 편의 시설
  - 주차: N
  - 와이파이: N
  - 장애인 편의시설: N
  - 반려동물 출입: N
  - 화장실: N

  ## 메뉴 정보
  - 외국어 메뉴 제공: N

  ## 주문 옵션
  - 배달 서비스: N
  - 배달앱 주문: N
  - 택배 판매: N
  - 모바일 결제: N
  - 온라인 예약: N
  "
  ```
- `RestaurantFinder.ipynb` 출력 결과
  ```
  사용자에게 보여줄 답변:
  부산에서 네이버 평점이 좋은 맛집을 추천해드리겠습니다.

  1. "한일돈까스": 부산광역시 사상구에 위치한 경양식 일반음식점으로, 네이버 평점이 4.4입니다. 매일 08:00부터 20:00까지 운영하며, 편의 시설은 제공되지 않습니다.

  2. "가장맛있는족발족과의동침(엄궁점)": 부산광역시 사상구에 위치한 일반음식점으로, 네이버 평점이 4.17입니다. 매일 15:00부터 23:59까지 운영하며, 주차와 와이파이 등의 편의 시설은 제공되지 않습니다.

  3. "명륜진사갈비(당감점)": 부산광역시 부산진구에 위치한 식육(숯불구이) 전문 식당으로, 네이버 평점이 4.15입니다. 평일에는 16:30부터 23:00까지, 공휴일에는 12:00부터 23:00까지 운영하며, 주차가 가능하고 배달 서비스도 제공됩니다.

  백엔드에 전달할 식당 ID:
  [579963, 687805, 29665]
  ```

## .md 형식만 가지고 있는 데이터
- `RAG_TEST_only_markdown.csv`
  ```
  947475,"# 감성키친(부산남구점)

  ## 기본 정보
  - 위치: 부산광역시 남구 유엔평화로14번길 54
  - 영업허가: 일반음식점
  - 지역: 부산광역시 남구

  ## 상세 설명
  부산광역시 남구에서 맛집을 찾으신다면 ""감성키친(부산남구점)""을 추천합니다.

  ## 운영 정보
  - 영업시간: 매일 10:00~22:00
  - 네이버 평점: 4.6300001

  ## 편의 시설
  - 주차: Y
  - 와이파이: N
  - 장애인 편의시설: N
  - 반려동물 출입: N
  - 화장실: N

  ## 메뉴 정보
  - 외국어 메뉴 제공: N

  ## 주문 옵션
  - 배달 서비스: N
  - 배달앱 주문: N
  - 택배 판매: N
  - 모바일 결제: N
  - 온라인 예약: N
  "
  ```
- `Only_MD.ipynb` 출력 결과
  ```
    사용자에게 보여줄 답변:
  부산에서 네이버 평점이 좋은 맛집을 추천드리겠습니다:

  1. "감성키친(부산남구점)": 이 식당은 부산광역시 남구에 위치하고 있으며, 네이버 평점이 4.63으로 높은 평가를 받고 있습니다. 매일 10:00부터 22:00까지 운영하며, 주차 시설이 제공됩니다.

  2. "청킹익스프레스": 부산광역시 부산진구에 위치한 이 식당은 네이버 평점이 4.25입니다. 주차, 와이파이, 장애인 편의시설 등은 제공되지 않지만, 맛집으로 추천할 만한 곳입니다.

  3. "명륜진사갈비(당감점)": 부산광역시 부산진구에 위치한 이 식당은 식육(숯불구이) 전문점으로, 네이버 평점이 4.15입니다. 평일과 공휴일에 영업시간이 다르며, 주차와 화장실 시설이 제공됩니다. 배달 서비스도 가능합니다.

  이 세 곳 모두 부산에서 맛집으로 추천할 만한 곳입니다.

  백엔드에 전달할 식당 ID:
  [966633, 947475, 687805]
  ``` 
## 비교 분석
#### "부산에서 네이버평점이 좋은 맛집을 추천해주세요." 라는 user_request에 대한 두 케이스의 출력 결과를 비교해보면, md 형식 데이터만 사용했을 때 더 높은 평점의 식당을 추천하는 경향이 있지만 더 테스트가 필요합니다.

## 앞으로 해야할 일
- 벡엔드에 보낼 식당ID를 추출법 수정
  - 현재 : retriever에 검색된 metadata를 가져오고 실제 답변에서 쓰이는 식당의 ID만을 추출할 때 문자열 안에 그 식당명이 있으면 추출하는 방법
  - 수정 할 점 : 메타데이터에서 바로 추출하는 방법
- 벡엔드 서버와 어떻게 통신할지 고민하기
- 벡엔드 서버와 실제로 데이터를 주고받는 것을 테스트하기

---

# 데이터 전처리 + 사용자 답변 & 벡엔드 연동 준비 (2024년 12월 27일)
[LangSmith Trace 보기](https://smith.langchain.com/public/ecb0236d-ac9c-4c31-8732-6371b2c1dc48/r)  

## 데이터 전처리
1. 기존 데이터에서 불필요한 열들은 제거하고 각 행마다 마크다운 형식으로 정리하였습니다.
2. 마크다운으로 정리된 데이터를 GPT API를 통해 요약하고 마크다운 데이터와 병합하였습니다.
3. 약 50000개의 데이터 중 100개를 랜덤으로 추출하였습니다.
4. 최종적으로 행(100) X 열(RSTR_ID,markdown_content) 형태가 되었습니다.


## 사용자 답변 & 벡엔드 연동 준비
- 사용자의 답변과 그 답변 안에서 언급되는 식당의 ID를 추출하였습니다.
- LangSmith를 보시면 사용자의 답변과 그 답변 안에서 언급되는 식당 ID를 잘 추출하는 것을 보입니다.

---

# 부산명소 국문 정보 + CoT & Few Shot 적용 (2024년 09월 04일)
[LangSmith Trace 보기](https://smith.langchain.com/public/3912cff7-4833-4294-b66e-a14a70e22437/r)  

## 문제 정의
LangChain의 Retriever를 통해 사용되는 인용 문서는 부산 트래블라운지를 기반으로 하지만, 최종 답변에서는 다음과 같은 부산의 주요 관광지와 음식점 정보가 검색되지 않는 문제가 있습니다:

- **관광지**:
  - 부산역
  - 용두산공원
  - 국제시장
  - 부산시민공원
  - 광안리 해수욕장

- **음식점**:
  - 이재모 피자
  - 할매가야밀면
  - 서면 쇼핑 거리
  - 돼지국밥집 '쌍둥이 돼지국밥'
  - 광안리 해변 근처 유명한 식당 '광안리 해물탕'

## 주요 문제점
- 관광지의 주소는 비교적 잘 표기되지만, 음식점의 이름과 주소는 환각 문제가 발생하고 있습니다.
