---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Data Model] TSK-DB-01: TENANT, USER, UPLOAD_LOG 스키마 구축"
labels: 'database, supabase, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-DB-01] 핵심 인증/로그 엔터티 DB 스키마 작성
- 목적: SaaS 멀티테넌트 환경의 기반이 되는 데이터베이스 구조를 Supabase PostgreSQL에 영속화한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#622-erd`](#)
- 태스크 명세: [`/wiki/concepts/architecture/TASKS/TASK-V1.0.md`](#)

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] `TENANT` 테이블 스키마 작성 (tenant_id PK, company_name, plan_tier, excel_mapping_rules JSONB)
- [ ] `USER` 테이블 스키마 작성 (user_id PK, tenant_id FK, email, hashed_password, forecast_purpose)
- [ ] `UPLOAD_LOG` 테이블 스키마 작성 (log_id PK, tenant_id FK, user_id FK, upload_time, is_success)
- [ ] 테이블 생성 및 FK 제약조건 설정을 위한 `.sql` 마이그레이션 스크립트 파일 작성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 스키마 생성 및 릴레이션 유효성
- Given: 작성된 DDL SQL 스크립트가 주어짐
- When: Supabase DB에 쿼리를 실행함
- Then: 에러 없이 3개의 테이블이 생성되며, `USER` 테이블에 `TENANT`를 참조하는 외래키(FK)가 강제된다.

## :gear: Technical & Non-Functional Constraints
- 보안: `excel_mapping_rules`는 확장성을 위해 반드시 `JSONB` 데이터 타입으로 선언한다.
- 보안: 외래키(FK) 릴레이션 시 `ON DELETE CASCADE` 등 데이터 삭제 정책을 명시한다.

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] SQL 스크립트가 문법적 오류(Lint) 없이 성공적으로 실행되는가?

## :construction: Dependencies & Blockers
- Depends on: None
- Blocks: TSK-DB-02, TSK-API-01, TSK-CMD-01
