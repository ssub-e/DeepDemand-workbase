---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-NFR-04: API 응답시간(p95 ≤ 1500ms) 및 예측 연산 지연시간 검증을 위한 k6 부하 테스트 스크립트 작성"
labels: 'qa/test, priority:medium'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-NFR-04] 부하 테스트 스크립트 작성
- 목적: 다수의 사용자가 동시에 예측을 트리거하거나 리스트를 조회할 때 시스템이 NFR(비기능 요구사항) 목표 성능을 유지하는지 검증한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev 단 노트: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#52`](#)
- TASK 메타데이터: `§5.2 (REQ-NF-01~04)`
- 선행 태스크: TSK-QRY-01

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] k6 기반의 부하 테스트 스크립트(`load-test.js`) 작성
- [ ] 가상 사용자(VU) 100명이 램프업(Ramp-up) 방식으로 `GET /status`, `POST /forecast/trigger` API를 동시 호출하는 시나리오 구성
- [ ] 응답 시간 p95 ≤ 1500ms 통과 기준(Thresholds) 설정

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 부하 상황 성능 목표 통과
- Given: 배포된 스테이징 백엔드 API
- When: k6 스크립트를 사용하여 100 VU로 5분간 부하를 발생시킴
- Then: 에러율이 1% 미만이며, 조회 API의 응답시간 p95가 1500ms 이하로 측정되어 스크립트가 Pass를 반환함.

## :gear: Technical & Non-Functional Constraints
- 독립성: 프로덕션 DB에 영향을 주지 않도록 반드시 Staging 또는 Test 환경에서 실행할 것

## :checkered_flag: Definition of Done (DoD)
- [ ] k6 스크립트가 작성되었고 테스트가 로컬/CI 환경에서 실행 가능한가?
- [ ] 테스트 결과 리포트(HTML/JSON)가 정상적으로 출력되는가?
