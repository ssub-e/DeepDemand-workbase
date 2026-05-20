---
type: concept
tags: [five-forces, market-analysis, business-strategy, saas, plg]
created: 2026-05-16
updated: 2026-05-16
---
# SaaS 타겟 5 Forces 분석 (PLG Pivot)

기존 B2B 특화 솔루션에서 벗어나, SME(중소상공인) 대상의 경량 SaaS 및 PLG(Product-Led Growth) 시장으로 진입하기 위한 마이클 포터의 5 Forces 프레임워크 기반 분석입니다.

## 1. 5 Forces 진단 요약

- **신규 진입자의 위협 (Medium)**
  - 낮은 기술적 진입 장벽: 오픈소스 시계열 예측 모델과 퍼블릭 클라우드의 발달로 초기 알고리즘 구축 비용이 낮음.
  - 높은 UX 장벽: 비전문가가 엑셀을 올리자마자 1분 안에 결과를 이해하게 만드는 '압도적으로 쉬운 UI/UX' 설계는 고도의 노하우가 필요함.
  - 네트워크 효과 부재: 1인 사용 툴이므로 초기 바이럴 기반의 방어벽 구축이 어려워 마케팅 투자가 필요함.

- **공급자의 교섭력 (Low)**
  - 인프라 완전 경쟁: AWS, Vercel 등 클라우드 호스팅 서비스는 완전 경쟁 상태이며 크레딧 지원이 풍부.
  - 다양한 데이터 API: 날씨, 트렌드 등의 API는 공공데이터 및 써드파티를 통해 저렴하게 교체 가능.
  - 결제망 종속성 미미: Stripe, Toss 등 PG사 역시 표준화된 수수료를 제공.

- **구매자의 교섭력 (High)**
  - 낮은 전환 비용(Switching Cost): API 연동 등 복잡한 구축이 없는 SaaS이므로, 쉽게 해지(Churn)하고 이탈하기 쉬움.
  - 극도의 가격 민감성: 월 구독료에 민감하므로 Freemium 모델이나 명확한 단기 ROI 입증이 필수.
  - 파편화된 구매자 풀: 고객이 소규모로 흩어져 있어 특정 고객에 휘둘리진 않으나 CAC(고객획득비용)가 높아질 위험.

- **대체재의 위협 (High)**
  - 수기 계산과 직감: 가장 강력한 대체재는 영세 사업자들의 기존 방식(엑셀 수기 계산, 감에 의존한 발주).
  - 플랫폼 내장 기능: Cafe24, 스마트스토어 등 플랫폼에 내장된 무료 판매 통계 대시보드.
  - 범용 재고 관리 툴: 바코드 스캔 중심의 가벼운 재고 관리 툴(박스히어로 등)의 예측 모듈 확장.

- **기존 경쟁자 간의 적대적 경쟁 (Medium)**
  - 블루오션 초기 단계: 초경량 AI 수요예측 SaaS 시장은 아직 절대 강자가 없는 초기 시장.
  - 마케팅 출혈 경쟁: 기술적 차별화보다는 CAC 최적화를 위한 퍼포먼스 마케팅 싸움으로 번질 가능성.

## 2. 핵심 성공 요인 (KSF - Key Success Factors)

1. **마찰 없는 온보딩 (Frictionless Onboarding)**: 영업 사원 개입 제로. 복잡한 연동 없이 과거 판매량 엑셀만 드래그 앤 드롭하면 60초 안에 첫 예측 리포트(Aha Moment) 제시.
2. **TTV(Time to Value) 극단적 단축**: 1%의 모델 정확도 향상보다 "내일 비가 오니 장화 발주를 30개 늘리세요"와 같은 즉각적 행동 지침(Actionable Insight) 제공이 중요.
3. **제품 주도 성장 (PLG) 루프 구축**: Freemium 요금제로 1개 SKU 예측을 무료로 제공하고, 자연스럽게 유료 결제 전환 유도.

## Related
- [B2B에서 범용 SaaS로의 전환 전략 (Pivot Strategy)](wiki/concepts/saas-pivot-strategy.md)
- [B2B 프레딕티브 AI 시장 5 Forces 분석 (Legacy)](wiki/concepts/business_strategy/five-forces-market.md)
