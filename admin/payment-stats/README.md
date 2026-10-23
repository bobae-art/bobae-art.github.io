# 이용권 결제 통계 관리자 화면

보배드림 매물등록 이용권 5종(대당 등록 / 5대 자유등록 / 딜러 1개월 / 상사 ~5명 / 상사 인원수 무제한)의
결제 현황을 집계하는 정적 대시보드입니다. 외부 라이브러리 없이 단일 `index.html`로 동작합니다.

- 배포 URL: https://bobae-art.github.io/admin/payment-stats/
- 기간(7일·30일·90일·이번 달·직접 지정) / 상품 / 결제상태 필터, KPI 타일(이전 기간 대비), 일별 추이,
  상품별 금액·건수, 결제수단 비중, 신규 vs 자동갱신, 결제 내역 검색·페이징, CSV 내보내기, 표 보기, 다크 모드

## 실데이터 연결

기본은 화면 검수용 **샘플 데이터**입니다. 다음 중 하나로 실데이터로 전환됩니다.

1. 같은 폴더에 `data.json` 업로드 (결제 건 배열, 또는 `{ "rows": [...] }`)
2. `index.html` 로드 전에 `window.PAYMENT_DATA_URL = "https://.../payments"` 지정 (CORS 허용 필요)

레코드 형식:

```json
{
  "id": "PY20261023001",
  "date": "2026-10-23",
  "time": "14:05",
  "product": "single | free5 | dealer | company5 | companyU",
  "amount": 11000,
  "method": "card | easy | transfer | vbank",
  "type": "new | renewal",
  "status": "paid | refunded | failed",
  "user": "bb****1234",
  "company": "서울오토갤러리"
}
```

`amount`가 없으면 상품 정가, `time`·`type`·`status`·`method`·`company`는 생략 시 기본값으로 채워집니다.
