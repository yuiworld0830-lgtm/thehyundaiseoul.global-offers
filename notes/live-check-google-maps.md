# 구글 지도 언어별 표시 라이브 체크

- **점검 시각(UTC):** 2026-11-22 05:38–05:43 (항목별 시각은 아래 표)
- **방법:** 미리 설치된 Playwright Chromium(headless) 사용. hl 값마다 브라우저 locale과 `Accept-Language` 헤더를 맞추고 `h1`, 카테고리 버튼, 주소 버튼(`aria-label`), 평점 블록을 읽음. 동의(consent) 페이지는 한 번도 뜨지 않음.
- **위치:** 컨테이너가 **미국 소재**이므로 한국에서 접속하면 결과가 다를 수 있음. 로그인하지 않은 상태라서 지도가 "제한된 뷰(limited view)"로 표시됨.
- **스크린샷:** `notes/screenshots/`
- 아래 내용은 페이지가 실제로 반환한 문자열만 옮긴 것임.

## 접속 경로 참고

- **A(더현대 서울):** `maps/search/?api=1&query=The+Hyundai+Seoul&hl=…` 는 4개 언어 모두 **단일 장소가 아닌 검색 결과 목록**을 반환함(`h1` 없음). 목록 1번째 항목은 언어별로 다음과 같음.
  - zh-TW / zh-CN / en: `The Hyundai Seoul`
  - ko: `더현대 서울`

  상세 정보를 보려고 해당 장소 URL(CID `0x357c9f007ca383cf:0xeb069748f6201a76`, `/g/11w3mh_j8v`)을 hl별로 직접 열었고, 아래 표의 A 행은 이 결과임.
- **B(티파니앤코):** search URL이 곧바로 장소 페이지로 이동함(CID `0x357b45c3d89d7801:0x7883571cabf15b8b`, `/g/11pqrg9sjd`).
- **구글 검색 지식패널** (`google.com/search?q=The+Hyundai+Seoul&hl=zh-TW`): **차단됨.** `/sorry/index` 로 리다이렉트되었고 "我們的系統偵測到您的電腦網路送出的流量有異常情況" 캡차가 떠서 지식패널은 렌더링되지 않음 (`Search_A_zh-TW_blocked.png`).

## 결과표

| 장소 | hl | 제목(h1) | 제목 아래 보조명 | 카테고리 | 주소(aria-label) | 평점 / 리뷰수 | 점검시각 UTC | 스크린샷 |
|---|---|---|---|---|---|---|---|---|
| A | zh-TW | `The Hyundai Seoul` | `더현대 서울` | `百貨公司` | `地址: 108 Yeoui-daero, Yeongdeungpo District, Seoul, 南韓` | 4.6 / 리뷰수 미표시 | 05:42:23 | A_zh-TW.png |
| A | zh-CN | `The Hyundai Seoul` | `더현대 서울` | `百货商场` | `地址: 108 Yeoui-daero, Yeongdeungpo District, Seoul, 韩国` | 4.6 / 미표시 | 05:42:28 | A_zh-CN.png |
| A | en | `The Hyundai Seoul` | `더현대 서울` | `Department store` | `Address: 108 Yeoui-daero, Yeongdeungpo District, Seoul, South Korea` | 4.6 / 미표시 | 05:42:33 | A_en.png |
| A | ko | `더현대 서울` | (없음) | `백화점` | `주소: 대한민국 서울특별시 영등포구 여의대로 108` | 4.6 / 미표시 | 05:42:38 | A_ko.png |
| B | zh-TW | `Tiffany & Co.` | `티파니앤코 더현대서울점` | `珠寶店` | `地址: The Hyundai Seoul 1F, 108 Yeoui-daero, Yeongdeungpo District, Seoul, 南韓` (所在地點：The Hyundai Seoul) | 4.4 / 미표시 | 05:40:16 | B_zh-TW.png |
| B | zh-CN | `Tiffany & Co.` | `티파니앤코 더현대서울점` | `珠宝行` | `地址: The Hyundai Seoul 1F, 108 Yeoui-daero, Yeongdeungpo District, Seoul, 韩国` (位于：The Hyundai Seoul) | 4.4 / 미표시 | 05:40:22 | B_zh-CN.png |
| B | en | `Tiffany & Co.` | `티파니앤코 더현대서울점` | `Jewelry store` | `Address: The Hyundai Seoul 1F, 108 Yeoui-daero, Yeongdeungpo District, Seoul, South Korea` (Located in: The Hyundai Seoul) | 4.4 / 미표시 | 05:40:27 | B_en.png |
| B | ko | `티파니앤코 더현대서울점` | (없음) | `귀금속 상점` | `주소: The Hyundai Seoul 1F, 108 여의대로 영등포구 서울특별시 대한민국` (위치: 더현대 서울) | 4.4 / 미표시 | 05:40:33 | B_ko.png |

리뷰수는 4개 언어 모두 표시되지 않았음. 비로그인 제한 뷰라서 평점 숫자만 노출됨.

### 최종 URL

- **A:** `https://www.google.com/maps/place/The+Hyundai+Seoul/data=!3m1!4b1!4m4!3m3!1s0x357c9f007ca383cf:0xeb069748f6201a76!16s%2Fg%2F11w3mh_j8v!20s8Q98GWGH%2BC87?hl=<LANG>&entry=ttu&g_ep=…`
  - ko만 경로 이름이 `%EB%8D%94%ED%98%84%EB%8C%80+%EC%84%9C%EC%9A%B8`(더현대 서울)로 바뀜.
- **B:** `https://www.google.com/maps/place/Tiffany+%26+Co./data=!3m1!4b1!4m4!3m3!1s0x357b45c3d89d7801:0x7883571cabf15b8b!16s%2Fg%2F11pqrg9sjd!20s8Q98GWGH%2BC8F?hl=<LANG>&entry=ttu&g_ep=…`
  - ko만 경로 이름이 `티파니앤코 더현대서울점`(URL 인코딩)으로 바뀜.

## 결론

1. **zh-TW에서 A가 "現代百貨 汝矣島店" 등으로 표시되는가?** → **아니요.**
   - 제목은 `The Hyundai Seoul`, 보조명은 `더현대 서울`임.
   - A 장소 페이지와 4개 언어의 검색 목록 어디에도 `現代百貨` / `汝矣島` 계열 문자열은 없었음.
   - 수집한 전체 텍스트에서 `現代`/`现代`/`汝矣`가 나온 곳은 단 1건임. zh-CN 검색 목록 중 별개 장소인 **버스 정류장** 이름 `The现代首尔`(카테고리 `公交车站`)이고, 백화점 프로필과는 관계없음.
2. **zh-TW에서 B의 이름에 현대 명칭이 들어가는가?** → **제목에는 들어가지 않음.**
   - 제목은 `Tiffany & Co.`뿐임.
   - 현대 명칭은 다음 위치에만 나타남.
     - 제목 아래 보조명 `티파니앤코 더현대서울점` (한글 그대로)
     - 주소 `The Hyundai Seoul 1F, …`
     - `所在地點：The Hyundai Seoul`
   - 중국어(번체) 현지화 명칭은 없음.
   - ko에서는 제목 자체가 `티파니앤코 더현대서울점`임.

※ 미국 IP·비로그인 상태에서 점검한 결과임. 한국 IP나 로그인 상태에서는 다르게 보일 수 있음.
