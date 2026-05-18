---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-CMD-07: 이력 기간 판별(14일) 기반 LightGBM 연산 및 Rule-based 안전재고 Fallback 분기 로직"
labels: 'feature, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-CMD-07] 예측 연산 및 Fallback 분기
- 목적: 충분한 판매 이력 유무에 따라 AI 모델링(LightGBM)과 규칙 기반(Rule-based) 연산을 동적으로 선택하여 예측 신뢰성을 보장한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#412`](#)
- TASK 메타데이터: `§4.1.2 (REQ-008,009)`
- 선행 태스크: TSK-CMD-06

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] 특정 SKU의 `DAILY_SALES_HISTORY` 데이터 카운트가 기준일(예: 14일) 이상인지 판별하는 로직
- [ ] 이력 충족 시: 외부 변수 피처와 결합하여 `LightGBM` 모델 추론 실행
- [ ] 이력 부족 시(Fallback): 최근 N일 평균 판매량 및 안전재고 계수를 사용한 Rule-based 연산 실행
- [ ] 연산 결과를 `FORECAST_RESULT` 테이블 DTO 포맷으로 가공

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 이력이 충분한 경우의 AI 모델 실행
- Given: 30일치 판매 이력을 가진 SKU
- When: 예측 로직이 해당 SKU를 평가함
- Then: LightGBM 추론 엔진이 호출되며, 모델이 반환한 예측 수요량이 결과로 할당됨.

Scenario 2: 콜드 스타트 SKU의 Rule-based Fallback
- Given: 판매 이력이 단 3일밖에 없는 신규 SKU
- When: 예측 로직이 해당 SKU를 평가함
- Then: 모델 대신 Rule-based 로직(최근 3일 평균 판매량 * 안전 계수)이 실행되어 결과가 할당됨.

## :gear: Technical & Non-Functional Constraints
- 성능: 다수 SKU 연산 시 Pandas Vectorization 등 배치(Batch) 처리 방식을 사용하여 연산 속도 최적화
- 데이터 정합성: Fallback 발생 시 결과 레코드에 `fallback_used: true` 플래그를 저장하여 추후 UI에서 렌더링되게 할 것

## :checkered_flag: Definition of Done (DoD)
- [ ] 두 가지 분기(AI, Fallback)가 모두 유닛 테스트로 검증되었는가?
- [ ] 연산 속도 저하를 막기 위해 Pandas/Numpy 기반의 효율적 연산이 적용되었는가?
