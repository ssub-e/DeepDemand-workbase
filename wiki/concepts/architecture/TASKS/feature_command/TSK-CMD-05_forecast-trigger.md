---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-CMD-05: 예측 시작 트리거 및 FastAPI BackgroundTasks 큐 할당 비즈니스 로직"
labels: 'feature, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-CMD-05] 예측 비동기 트리거
- 목적: 무거운 예측 모델 연산을 백그라운드 태스크로 할당하여 API 응답 지연을 방지하고 유연한 예측 파이프라인을 구축한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#412-예측-모델링-forecast`](#)
- TASK 메타데이터: `§4.1.2 (REQ-007)`
- 선행 태스크: TSK-CMD-04

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] `POST /forecast/trigger` 엔드포인트 비즈니스 로직 구현
- [ ] 요청 Payload에서 Tenant 및 대상 SKU 정보 파싱 및 검증
- [ ] `FastAPI BackgroundTasks` 또는 메시지 큐(Celery/Redis 등)에 연산 작업 적재
- [ ] 작업 상태(Status)를 DB 또는 캐시에 'PENDING'으로 초기화 및 Task ID 발급 반환

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 정상적인 예측 트리거
- Given: 데이터 업로드가 완료된 유효한 대상 SKU 리스트
- When: `/forecast/trigger` API를 호출함
- Then: 202 Accepted 상태코드와 함께 Task ID를 반환하며, 백그라운드 큐에 작업이 정상 적재되어야 함.

Scenario 2: 데이터 미비 시 트리거 거부
- Given: `DAILY_SALES_HISTORY`에 이력 데이터가 없는 SKU
- When: `/forecast/trigger` API를 호출함
- Then: 400 Bad Request 상태코드와 함께 "이력 데이터가 부족합니다"라는 에러 메시지 반환.

## :gear: Technical & Non-Functional Constraints
- 성능: API 자체의 응답 시간은 비동기 처리를 통해 p95 ≤ 200ms 이내 보장
- 안정성: 큐 적재 실패 시 적절한 예외 처리 및 로깅 적용
- 확장성: 향후 대규모 분산 처리 시스템으로 이전하기 쉬운 큐 추상화 계층 고려

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] 단위 테스트(Unit Test) 및 통합 테스트(Integration Test)가 추가되었고 통과하는가?
- [ ] SonarQube / Linter 등의 정적 분석 도구 경고가 없는가?
- [ ] API 명세서(Swagger 등)가 최신화되었는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-CMD-04 (데이터 인서트 완료)
- Blocks: TSK-CMD-06 (외부 데이터 수집 로직)
