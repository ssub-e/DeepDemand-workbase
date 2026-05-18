---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[QA/Test] TSK-TST-01: 파일 검증 및 예외 처리(400 에러) 단위 테스트"
labels: 'test, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-TST-01] 파싱 실패 및 누락 데이터 예외 상황 단위 테스트 작성
- 목적: AI 에이전트가 작성한 백엔드 업로드 로직(TSK-CMD-02, 03)이 기획 인수 조건(AC)을 완벽히 만족하는지 자동 검증하는 척도를 마련한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#51-functional-verification-matrix`](#)

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] `pytest` 및 `httpx` (또는 `TestClient`) 테스트 환경 구성
- [ ] 빈 파일(0 byte) 업로드 시 400 Bad Request 에러 반환 검증 코드 작성
- [ ] 엑셀 파일 내 필수 컬럼(상품명, 옵션명 등) 누락 시 200 OK + `missing_rows_count` 반환 여부 검증 코드 작성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 자동 테스트 실행 검증
- Given: 파싱 비즈니스 로직(TSK-CMD-03)이 완성된 상태의 FastAPI 앱
- When: `pytest tests/test_upload.py` 명령어를 실행함
- Then: 작성된 예외 상황 시나리오 2건이 모두 `PASS` 처리되어야 한다.

## :gear: Technical & Non-Functional Constraints
- 성능: 업로드 및 에러 반환을 검증하는 테스트 코드의 실행(Assert) 소요 시간은 건당 1000ms 이하로 동작해야 한다.

## :checkered_flag: Definition of Done (DoD)
- [ ] 테스트 커버리지가 업로드 및 검증 컨트롤러 로직의 80% 이상을 덮는가?
- [ ] Pytest 실행 시 에러 없이 통과하는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-CMD-03 (검증할 타겟 로직)
- Blocks: 전체 기능 안정화 단계
