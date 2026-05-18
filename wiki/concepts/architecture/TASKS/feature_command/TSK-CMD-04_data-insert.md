---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-CMD-04: 파싱 성공 데이터 DAILY_SALES_HISTORY 및 UPLOAD_LOG 누적 인서트(Append) 로직"
labels: 'feature, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-CMD-04] 파일 파싱 결과 DB 영속화
- 목적: 검증이 완료된 엑셀/CSV 데이터를 데이터베이스에 성공적으로 누적 삽입(Append)하고 업로드 이력을 남긴다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#411-데이터-수집-및-전처리-ingestion`](#)
- TASK 메타데이터: `§4.1.1 (REQ-016,017)`
- 선행 태스크: TSK-CMD-03, TSK-DB-02

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] `DAILY_SALES_HISTORY` 테이블에 대량 데이터 Bulk Insert 로직 구현
- [ ] `UPLOAD_LOG` 테이블에 업로드 성공/실패 메타데이터 저장 로직 구현
- [ ] 중복 데이터(동일 날짜/SKU) 인서트 시 처리 전략(Upsert 등) 적용
- [ ] 트랜잭션(Transaction) 처리로 데이터 정합성 보장 로직 구현

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 정상적인 데이터 인서트
- Given: 검증을 통과한 5,000건의 판매 이력 데이터가 주어짐
- When: DB 인서트 모듈을 실행함
- Then: `DAILY_SALES_HISTORY`에 5,000건이 모두 저장되고 `UPLOAD_LOG`에 성공 이력이 정상적으로 남아야 함.

Scenario 2: 중복 데이터(동일 날짜/SKU) 존재 시 병합
- Given: 이미 DB에 존재하는 특정 날짜와 SKU의 판매 데이터가 주어짐
- When: 동일한 날짜/SKU에 대한 새로운 판매 데이터가 인서트됨
- Then: 기존 데이터가 덮어씌워지거나(Upsert) 지정된 병합 규칙에 따라 처리되어 DB 에러가 발생하지 않아야 함.

## :gear: Technical & Non-Functional Constraints
- 성능: Bulk Insert 최적화를 통해 10,000건 처리에 3초 이내 달성
- 안정성: 인서트 도중 일부 실패 시 전체 롤백(Rollback) 처리
- 보안: 쿼리 실행 시 SQL Injection 방지 (ORM 또는 Parameterized Query 사용)

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] 단위 테스트(Unit Test) 및 통합 테스트(Integration Test)가 추가되었고 통과하는가?
- [ ] SonarQube / Linter 등의 정적 분석 도구 경고가 없는가?
- [ ] API 명세서(Swagger 등)가 최신화되었는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-CMD-03 (컬럼 매핑 및 검증), TSK-DB-02 (스키마 작성)
- Blocks: TSK-CMD-05 (예측 시작 트리거)
