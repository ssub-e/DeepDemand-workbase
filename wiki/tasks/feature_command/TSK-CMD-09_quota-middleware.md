---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-CMD-09: 테넌트 Plan 기반 SKU 예측 한도(Quota) 검증 및 차단(403) 미들웨어 구현"
labels: 'feature, backend, priority:medium'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-CMD-09] 구독 플랜 기반 Quota 제어
- 목적: 각 테넌트(사용자 회사)의 플랜(Free, Pro 등)에 따라 허용된 SKU 예측 한도를 통제하여 수익화(Monetization) 기반을 마련한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#412`](#)
- TASK 메타데이터: `§4.1.2 (REQ-023)`
- 선행 태스크: TSK-DB-01, TSK-API-02

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] JWT 내 Tenant ID를 기반으로 해당 테넌트의 구독 Plan(할당량)을 DB 또는 캐시에서 조회
- [ ] 예측 API 트리거 시 요청된 SKU 개수와 이번 달 사용량(Usage)을 비교하는 로직 구현
- [ ] 한도 초과 시 요청을 중단하고 403 Forbidden 상태와 안내 메시지를 반환하는 미들웨어/의존성 주입(Dependency) 구현

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 한도 내 정상 호출
- Given: 월 10,000 SKU 한도를 가진 Pro 테넌트 (현재 사용량: 5,000)
- When: 1,000 SKU 예측을 트리거함
- Then: 미들웨어 검증을 통과하고 비즈니스 로직으로 정상 인가(Authorize)됨.

Scenario 2: 한도 초과 차단
- Given: 1 SKU 한도를 가진 Free 테넌트
- When: 2 SKU 예측을 트리거함
- Then: 즉시 403 상태 코드가 반환되며 예측 로직이 실행되지 않음.

## :gear: Technical & Non-Functional Constraints
- 성능: 매 요청마다 DB 조회를 방지하기 위해 Redis 등을 활용한 테넌트 플랜 정보 캐싱(Caching) 적용 권장

## :checkered_flag: Definition of Done (DoD)
- [ ] 미들웨어 단위 테스트가 성공적으로 작성되었는가?
- [ ] 예외 응답 형식이 팀이 정의한 글로벌 에러 포맷을 준수하는가?
