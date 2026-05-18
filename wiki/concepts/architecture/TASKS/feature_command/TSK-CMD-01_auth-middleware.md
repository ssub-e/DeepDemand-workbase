---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-CMD-01: [Feature/Command] JWT 기반 로그인 인증 로직 및 Tenant ID 검증 미들웨어 구현"
labels: 'feature, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-CMD-01] JWT 인증 및 Tenant 미들웨어
- 목적: 사용자 로그인을 처리하여 JWT를 발급하고, 이후 요청에서 JWT를 기반으로 사용자 인증 및 Tenant 권한(데이터 격리)을 검증한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#415`](#) (REQ-015)
- 의존성 태스크: TSK-DB-01, TSK-API-01

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] 로그인 로직 (ID/PW 검증 및 JWT 발급) 구현
- [ ] API 요청 헤더의 JWT 추출 및 검증 로직 작성
- [ ] 요청 컨텍스트에서 Tenant ID 추출 및 접근 권한 검증을 수행하는 미들웨어/인터셉터 구현
- [ ] 단위 및 통합 테스트 코드 작성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 올바른 계정으로 로그인 성공
- Given: 데이터베이스에 등록된 유효한 ID/PW가 주어짐
- When: `/login` API를 호출함
- Then: 200 상태 코드와 함께 JWT Access Token을 반환한다.

Scenario 2: 권한 없는 Tenant 데이터 접근 차단
- Given: Tenant A에 속한 사용자의 유효한 JWT
- When: Tenant B의 리소스에 접근 시도
- Then: Tenant 미들웨어에서 권한 없음을 감지하여 403 Forbidden 상태 코드를 반환한다.

## :gear: Technical & Non-Functional Constraints
- 보안: JWT Secret Key는 환경 변수에서 주입하며, 토큰 만료 시간 설정 필수

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] 단위/통합 테스트 통과 및 테스트 커버리지를 만족하는가?
- [ ] Tenant 기반 데이터 격리 로직이 미들웨어로 분리되어 있는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-DB-01, TSK-API-01
- Blocks: TSK-TST-03
