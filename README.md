# 디딤돌·보금자리론 금리 자료

이 저장소는 디딤돌대출·보금자리론 앱이 공통으로 읽는 공개 금리 파일과 웹 앱 사본을 둡니다.

- 금리 파일: [rates.json](./rates.json)
- 웹 주소: https://nhfc100-boop.github.io/loan-rates/
- 금리우대 알아보기: https://nhfc100-boop.github.io/loan-rates/woodae/
- 금리·한도 계산기: https://nhfc100-boop.github.io/loan-rates/calc/
- KB시세 LTV 계산기: https://nhfc100-boop.github.io/loan-rates/kb-ltv/

앱은 실행될 때 `rates.json`을 내려받아 금리를 갱신합니다. 인터넷이 없으면 기기에 저장된 직전 파일, 그것도 없으면 앱에 들어 있는 기본 금리를 씁니다. 이용자가 입력한 값은 전송하지 않습니다.

`schemaVersion`은 현재 `1`입니다. 앱은 이 값이 `1`이고 금리표 모양이 맞을 때만 파일을 받아들입니다.

## 매월 금리 업데이트

자세한 절차는 [UPDATE.md](./UPDATE.md)를 따르세요. 요약하면 다음과 같습니다.

1. 한국주택금융공사 보금자리론 금리 안내와 디딤돌 금리 안내 페이지에서 공시 금리를 확인합니다.
2. `rates.json`의 해당 칸과 `didimdolBaseDate`, `bogeumjariBaseDate`, `didimAsOf`, `bogeumAsOf`, `updatedAt`을 고칩니다.
3. 숫자를 추측하지 말고, 공식 페이지에 있는 값만 넣습니다.
4. `git add rates.json` 후 커밋하고 `main` 브랜치에 push하면 GitHub Pages가 파일을 갱신합니다.
5. 앱을 다시 설치하지 않아도, 다음에 앱을 열 때 새 금리를 읽습니다.

우대 규칙이나 소득 한도처럼 계산 방식 자체가 바뀌면 `rates.json`만으로는 부족할 수 있습니다. 그때는 앱 화면을 고친 뒤 다시 올려야 합니다.

## 출처

- 디딤돌 금리안내: https://www.hf.go.kr/ko/sub01/sub01_02_03.do
- 디딤돌 상품소개: https://hf.go.kr/ko/sub01/sub01_02_01.do
- 보금자리론 금리안내: https://www.hf.go.kr/ko/sub01/sub01_01_04.do
- 보금자리론 상품소개: https://hf.go.kr/ko/sub01/sub01_01_01.do
- 주택도시기금: https://nhuf.molit.go.kr

본 자료는 공식 기관의 앱이 아니며 참고용입니다.
