---
type: concept
tags: [strategy, pivot, saas, plg]
created: 2026-05-16
updated: 2026-05-16
---

# B2B 컨셉에서 범용 AI 수요예측 SaaS로의 전환 전략

DeepDemand를 현재의 특정 B2B(Enterprise-heavy) 중심 솔루션에서 범용 AI 수요예측 SaaS로 전환하기 위한 핵심 전략과 실행 계획입니다.

## 1. 전략적 전환 (Strategic Shift)

| 구분 | 현재 (B2B/Custom) | 전환 후 (Simple SaaS/PLG) |
| :--- | :--- | :--- |
| **핵심 가치** | 결재 방어, 인건비 최적화 (특수 목적) | 누구나 쉽게 시작하는 AI 수요 예측 (범용) |
| **타겟** | 중대형 이커머스 MD, 3PL 센터장 | 소상공인, 리테일 매장 점주, 1인 셀러 |
| **진입 장벽** | API 연동 필수, 영업 상담 필요 | CSV 업로드 즉시 분석, 무료 체험(Freemium) |
| **성공 지표** | 도입 후 비용 절감액 (ROI) | 첫 예측 리포트 생성까지 걸리는 시간 (TTV) |

## 2. 기술 및 기능적 필수 작업

### 2.1 데이터 인입의 범용화 (Data Democratization)
- **CSV/Excel 드래그 앤 드롭 업로드**: 별도 연동 없이도 과거 판매 데이터를 업로드하면 즉시 분석이 시작되어야 함.
- **데이터 매핑 자동화**: 사용자가 올린 엑셀 컬럼(날짜, 판매량, 상품명 등)을 AI가 자동으로 인식하도록 매퍼(Mapper) UI 강화.

### 2.2 온보딩 프로세스 간소화 (Frictionless Onboarding)
- **Step 1**: "무엇을 예측하고 싶으신가요?" (매출, 재고 부족, 필요 인력 중 선택)
- **Step 2**: "데이터를 올려주세요" (CSV 업로드 섹션 강조)
- **Step 3**: "분석 완료" (대시보드로 즉시 진입하여 가치 체감)

### 2.3 대시보드 UI/UX 단순화
- **요약 카드 중심**: 복잡한 PDF 리포트보다는 화면 내에서 "내일 예상 판매량은 120건입니다"와 같은 직관적 카드 전면 배치.
- **알림 체계(Alert System)**: "주의: 3일 내 품절 예상 품목 5개"와 같은 즉각적 액션 아이템 중심 개편.

### 2.4 구독 모델 및 결제 시스템 도입
- **Tiered Pricing**: Free (1개 SKU), Basic (100개 SKU), Pro (무제한) 등 SKU 수나 예측 횟수 기반 요금제 설계.
- **Self-Service Billing**: 사용자가 설정 페이지에서 직접 카드 등록 및 결제가 가능하도록 연동.

## 3. 단계별 로드맵 (Action Plan)

1. **Phase 1: Zero-Touch Entry**
   - `Onboarding.tsx`에 CSV 업로드 기능 추가.
   - 랜딩 페이지 메시지를 보편적 가치(성장, 비용 절감) 중심으로 수정.
2. **Phase 2: Product-Led Growth**
   - 대시보드에서 3PL 전용 기능을 위젯화하여 필요 시에만 활성화.
   - 무료 체험판을 위한 데이터 격리 및 멀티테넌시 구조 최적화.
3. **Phase 3: Monetization**
   - Stripe/Toss Payments 등 결제 게이트웨이 연동.
   - 요금제별 기능 제한 및 사용량 트래킹 시스템 구축.

## Related
- [가치 제안 및 Feature Map](wiki/concepts/value-proposition.md)
- [비즈니스 전략 개요](wiki/concepts/business_strategy/value-chain-strategy.md)
- [핵심 페르소나](wiki/entities/personas.md)
