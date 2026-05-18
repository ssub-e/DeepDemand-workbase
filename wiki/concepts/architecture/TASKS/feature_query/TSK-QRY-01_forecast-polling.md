---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-QRY-01: GET /status 폴링 응답 및 SKU별 발주 추천 리스트, 신뢰도/품절경고 지표 조회 로직"
labels: 'feature, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-QRY-01] 발주 추천 리스트 데이터 제공 API
- 목적: 프론트엔드의 대시보드 화면에 최종적으로 계산된 발주 추천 목록, 상태 정보, XAI 지표 등을 응답(Read)으로 제공한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#412`](#)
- TASK 메타데이터: `§4.1.2 (REQ-010,011)`
- 선행 태스크: TSK-DB-02, TSK-API-02

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] Task ID를 이용한 예측 진행 상태(PENDING, PROCESSING, SUCCESS) 폴링용 `GET /forecast/status` 엔드포인트 구현
- [ ] 예측 완료 후, `FORECAST_RESULT` 및 `XAI_FACTOR`를 Join하여 종합 데이터를 반환하는 `GET /forecast/recommendations` 구현
- [ ] 대용량 리스트 조회를 위한 페이지네이션(Pagination) 및 정렬(위험도 순, 발주량 순) 로직 추가

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 예측 리스트 정상 조회
- Given: 특정 테넌트의 예측 연산이 완료된(SUCCESS) 상태
- When: `/forecast/recommendations?page=1` API를 호출함
- Then: 200 OK와 함께 SKU별 추천 발주량, 현재 재고, 품절 위험도, XAI 텍스트가 포함된 JSON 리스트가 반환됨.

## :gear: Technical & Non-Functional Constraints
- 성능: 다중 테이블 Join 조회 시 성능 최적화를 위해 적절한 DB Index 설정
- 보안: 다른 테넌트의 데이터가 조회되지 않도록 WHERE 조건에 철저한 Tenant ID 격리 처리 필수

## :checkered_flag: Definition of Done (DoD)
- [ ] API 반환값이 Swagger DTO 명세와 일치하는가?
- [ ] 다량의 데이터(1만건) 조회 시 500ms 이내에 응답이 오는가?
