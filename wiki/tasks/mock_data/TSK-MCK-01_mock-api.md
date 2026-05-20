---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-MCK-01: 프론트엔드 UI 개발용 발주 추천 결과 및 403 에러 Mocking API 세팅"
labels: 'mock_data, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-MCK-01] UI 개발용 API Mocking
- 목적: 백엔드 개발이 완료되기 전 프론트엔드 팀이 병렬적으로 UI/UX 개발을 진행할 수 있도록 가상의 API 응답을 제공한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#61`](#)
- TASK 메타데이터: `§6.1 (API-05)`
- 선행 태스크: TSK-API-02

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] MSW(Mock Service Worker) 라이브러리 설치 및 초기 세팅
- [ ] `GET /forecast/recommendations` 등의 정상 200 OK 더미 데이터(JSON) 작성
- [ ] Quota 초과 시나리오 재현을 위한 403 Forbidden 에러 응답 핸들러 추가
- [ ] 네트워크 지연(Delay) 설정을 통한 로딩(Skeleton UI) 테스트 환경 구성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 정상 Mock 데이터 호출
- Given: 브라우저에 MSW가 구동 중인 프론트엔드 개발 환경
- When: 클라이언트가 `/forecast/recommendations` API를 호출함
- Then: 백엔드 서버 없이도 사전에 정의된 추천 리스트 Mock JSON 데이터가 반환됨.

## :gear: Technical & Non-Functional Constraints
- 호환성: 실제 백엔드 DTO(TSK-API-02) 규약과 100% 일치하는 스키마 구조를 가질 것

## :checkered_flag: Definition of Done (DoD)
- [ ] 프론트엔드 브라우저 콘솔에 MSW 구동 메시지가 표시되는가?
- [ ] API 호출 시 올바른 타입의 Mock 데이터가 반환되는가?
