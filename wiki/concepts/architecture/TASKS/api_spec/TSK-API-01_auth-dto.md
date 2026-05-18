---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[API Spec] TSK-API-01: Auth 도메인 DTO 및 예외 코드 정의"
labels: 'api, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-API-01] 로그인/인증 도메인 Request/Response DTO 정의
- 목적: 프론트엔드와 백엔드가 데이터 포맷과 에러 코드를 일치시키기 위한 단일 진실 공급원(Contract)을 수립한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#61-api-엔드포인트-목록`](#)

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] Pydantic을 이용한 `LoginRequest` DTO 작성 (email, password 필드 검증)
- [ ] Pydantic을 이용한 `LoginResponse` DTO 작성 (access_token, token_type, user_id, tenant_id)
- [ ] `AuthException` 공통 예외 클래스 및 에러 코드(401 Unauthorized, 404 Not Found) 정의

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: DTO Validation 검증
- Given: 이메일 형식이 아닌 문자열(`testexample.com`)이 주어짐
- When: `LoginRequest` DTO에 주입하여 검증함
- Then: Pydantic Validation Error가 발생하며 "유효한 이메일 형식이 아닙니다"를 반환한다.

## :gear: Technical & Non-Functional Constraints
- 설계: DTO 내부 로직에 데이터베이스 쿼리나 서비스 비즈니스 로직을 포함시켜서는 절대 안 된다. 오직 데이터의 '형태(Shape)'만 정의한다.

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] 프론트엔드가 참조할 수 있는 Swagger(OpenAPI) 문서에 DTO 스키마가 정상 표출되는가?

## :construction: Dependencies & Blockers
- Depends on: None
- Blocks: TSK-CMD-01
