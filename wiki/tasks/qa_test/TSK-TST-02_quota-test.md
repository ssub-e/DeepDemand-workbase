---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-TST-02: Free 유저 1 SKU 초과 예측 트리거 시 403 Forbidden 차단(AC) 단위 테스트"
labels: 'feature, qa/test, priority:medium'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-TST-02] Quota 초과 검증 단위/통합 테스트
- 목적: Free 플랜 등급의 사용자가 시스템에서 허용된 할당량(Quota, 1 SKU)을 초과하여 예측 연산을 요청할 때 정확히 인가(Authorization) 차단이 일어나는지 검증한다.

## :link: References (Spec & Context)
> :bulb: AI 연동 시 참조: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#51-인수-테스트-조건-ac`](#)
- TASK 메타데이터: `§5.1 (TC-F23)`
- 선행 태스크: TSK-CMD-09 (Quota 미들웨어 구현)

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] 테스트 환경용 Free 플랜 Tenant 및 JWT 토큰 Mock 데이터 셋업
- [ ] 2개 이상의 SKU 리스트를 Payload로 담아 `/forecast/trigger` 엔드포인트에 요청하는 테스트 케이스 작성 (Pytest 등 활용)
- [ ] 반환된 Response Status Code가 HTTP 403 Forbidden인지 확인하는 Assertion 작성
- [ ] 응답 에러 메시지(Body)에 Quota 초과 안내 및 플랜 업그레이드 권유 내용이 포함되어 있는지 정규식 등으로 검증
- [ ] DB 상태 롤백(Rollback) 및 테스트 간 격리성 보장 로직 구성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 허용량 초과 요청의 정확한 차단
- Given: 1 SKU 예측만 허용된 Free Plan 유저의 유효한 인증 토큰
- When: 2개 이상의 SKU에 대한 예측을 동시에 요청함
- Then: 서버는 백그라운드 큐에 작업을 적재하지 않고 즉시 403 상태 코드와 지정된 예외 메시지를 반환함.

Scenario 2: 허용량 이내 요청의 정상 처리
- Given: 동일한 Free Plan 유저 인증 토큰
- When: 정확히 1개의 SKU에 대한 예측을 요청함
- Then: 서버는 요청을 정상 수락하고 202 Accepted와 함께 큐에 작업을 적재함.

## :gear: Technical & Non-Functional Constraints
- 독립성: 다른 단위 테스트 및 통합 테스트 케이스의 DB/Cache 상태에 전혀 영향을 주지 않아야 함 (테스트 픽스처 활용 철저)
- 커버리지: 미들웨어 및 예외 처리 컨트롤러의 코드 커버리지가 해당 테스트를 통해 90% 이상 도달해야 함

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria(테스트 케이스)가 CI 환경에서 성공적으로 통과(Pass)하는가?
- [ ] 테스트 실행 시간이 과도하게 길지 않은가? (단일 단위 테스트 기준 500ms 이내)
- [ ] 에지 케이스(정확히 1개 요청, 0개 요청 등)에 대한 테스트도 작성되었는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-CMD-09 (테넌트 Plan 기반 SKU 예측 한도 검증 로직 완료)
- Blocks: CI/CD 파이프라인 무결성 검증 통과 단계
