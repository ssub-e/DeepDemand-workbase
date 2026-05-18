---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-DB-02: [DB] DAILY_SALES_HISTORY, FORECAST_RESULT, SKU_METRICS, XAI_FACTOR 스키마 작성"
labels: 'feature, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-DB-02] 예측결과 및 히스토리 DB 스키마 작성
- 목적: 수요 예측을 위한 이력 데이터 및 결과 데이터를 저장하기 위한 테이블 구조를 Supabase SQL로 정의한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#622`](#)
- 의존성 태스크: TSK-DB-01

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] `DAILY_SALES_HISTORY` 테이블 스키마 작성
- [ ] `FORECAST_RESULT` 테이블 스키마 작성
- [ ] `SKU_METRICS` 테이블 스키마 작성
- [ ] `XAI_FACTOR` 테이블 스키마 작성
- [ ] 각 테이블에 대한 `TENANT_ID` 외래키 등 제약조건 적용 스크립트 작성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 데이터베이스 마이그레이션 실행
- Given: TSK-DB-01이 완료되어 기본 테이블들이 생성된 상태
- When: 마이그레이션 스크립트를 Supabase에 적용함
- Then: `DAILY_SALES_HISTORY`, `FORECAST_RESULT`, `SKU_METRICS`, `XAI_FACTOR` 테이블이 정상적으로 생성된다.

## :gear: Technical & Non-Functional Constraints
- 보안: RLS (Row Level Security) 적용 필수

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] 마이그레이션 SQL 스크립트가 작성되었는가?
- [ ] Supabase 환경에 성공적으로 적용되는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-DB-01
- Blocks: TSK-CMD-04, TSK-QRY-01
