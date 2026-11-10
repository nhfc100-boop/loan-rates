# 월간 금리 업데이트 절차

앱을 다시 빌드하거나 Play 스토어에 올리지 않아도, 이 저장소의 `rates.json`만 고치면 다음 실행부터 새 금리가 반영됩니다.

작업은 매월 1일(또는 공시가 나온 직후)에 하면 됩니다. 숫자는 추측하지 말고 공식 페이지에 적힌 값만 옮기세요.

## 1. 공식 페이지 확인

브라우저에서 아래 페이지를 엽니다.

1. 보금자리론 금리 안내  
   https://www.hf.go.kr/ko/sub01/sub01_01_04.do  
   - 확인할 것: 아낌e보금자리론 10·15·20·30·40·50년 금리, 공시일(적용일)  
   - `u-보금자리론` / `t-보금자리론` 표가 있으면 함께 적습니다. 앱의 `bogeumU`에 해당합니다.

2. 디딤돌대출 금리 안내  
   https://www.hf.go.kr/ko/sub01/sub01_02_03.do  
   - 확인할 것: 일반 가구 표, 생애최초 신혼 전용 표  
   - 소득 구간: 2천만 원 이하(`b20`), 2천만 초과~4천만(`b40`), 4천만 초과~7천만(`b70`), 7천만 초과~8,500만(`b85`)  
   - 만기: 10·15·20·30년  
   - 공시일(적용일)

참고로 볼 수 있는 페이지:

- 디딤돌 상품소개 https://hf.go.kr/ko/sub01/sub01_02_01.do
- 보금자리론 상품소개 https://hf.go.kr/ko/sub01/sub01_01_01.do
- 주택도시기금 https://nhuf.molit.go.kr  
  (기금 포털 표가 열리면 주금공 표와 비교합니다. 값이 다르면 추측하지 말고 주금공 공시를 우선하되, 차이를 메모합니다.)

## 2. rates.json 수정

저장소를 받은 뒤 `rates.json`을 엽니다.

- `schemaVersion`은 `1`로 그대로 둡니다. 앱이 이 값이 `1`인지 확인합니다.
- `didimdolBaseDate`, `didimAsOf`: 디딤돌 공시일 (`YYYY-MM-DD`, 예: `2026-11-01`)
- `bogeumjariBaseDate`, `bogeumAsOf`: 보금자리론 공시일 (예: `2026-11-09`)
- `updatedAt`: 파일을 고친 시각 (아시아/서울, ISO 8601, 예: `2026-12-01T09:15:00+09:00`)
- `checkedOn`: 확인한 날짜 (`YYYY-MM-DD`)
- `didimGeneral`, `didimNewlyFirst`: 소득 구간 × 만기 기본금리
- `bogeumE`: 아낌e 만기별 금리
- `bogeumU`: u·t 만기별 금리
- 우대 %p, 상한, 최저금리, 소득 한도는 공시에 변경이 있을 때만 고칩니다.

JSON 모양이 깨지지 않게 따옴표와 쉼표를 유지하세요. 금리 칸은 소수 둘째 자리(예: `5.00`, `3.85`)로 적는 것이 좋습니다.

## 3. 저장하고 올리기

```bash
cd loan-rates
git add rates.json
git commit -m "Update rates for YYYY-MM (디딤돌 YYYY-MM-DD, 보금자리론 YYYY-MM-DD)"
git push origin main
```

수 분 안에 https://nhfc100-boop.github.io/loan-rates/rates.json 이 새 내용으로 바뀝니다. 브라우저에서 파일을 열어 `updatedAt`과 금리 칸을 확인하세요.

## 4. 앱에서의 확인

웹 앱이나 안드로이드 앱을 연 뒤 상태 문구가 `최신 금리 반영됨`인지, `금리 기준일`이 새 공시일과 같은지 확인합니다.

우대 항목 신설·폐지, 소득 한도 변경, 만기 추가처럼 계산 규칙이 바뀌면 `rates.json`만으로는 부족합니다. 그때는 앱 코드를 수정한 뒤 다시 배포해야 합니다.
