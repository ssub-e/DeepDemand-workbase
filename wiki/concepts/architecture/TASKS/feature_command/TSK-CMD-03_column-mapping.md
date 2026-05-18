---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-CMD-03: [Feature/Command] 필수 컬럼 정규식 매핑 검증 및 excel_mapping_rules 영속화 분기 처리 로직"
labels: 'feature, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-CMD-03] 데이터 컬럼 정규식 맵핑 및 규칙 저장
- 목적: 업로드된 파일의 컬럼명이 시스템 필수 컬럼(상품코드, 날짜, 판매량 등)과 일치하는지 정규식 기반으로 자동 맵핑하고, 사용자가 확정한 맵핑 룰을 다음 업로드 시 재사용하기 위해 DB에 영속화한다.

## :link: References (Spec & Context)
> :bulb: AI 연동 & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#411`](#) (REQ-004,005)
- 의존성 태스크: TSK-CMD-02

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] 필수 컬럼을 찾기 위한 정규식 패턴 세트 정의
- [ ] 파일의 헤더를 분석하여 자동 맵핑 수행 비즈니스 로직 작성
- [ ] 자동 맵핑 실패 또는 사용자 수동 맵핑 수정 분기 처리
- [ ] 맵핑 결과(`excel_mapping_rules`)를 데이터베이스(Tenant 설정 등)에 업데이트하는 로직 구현

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 자동 맵핑 및 룰 저장
- Given: '상품ID', '일자', '수량'이라는 헤더를 가진 파일이 업로드됨
- When: 자동 매핑을 실행함
- Then: 정규식에 의해 각각 SKU, DATE, SALES로 자동 맵핑되며, 변경된 룰을 `excel_mapping_rules`에 성공적으로 저장한다.

Scenario 2: 필수 컬럼 누락
- Given: '판매량'을 유추할 수 없는 헤더를 가진 파일이 업로드됨
- When: 자동 매핑을 실행함
- Then: 필수 컬럼이 누락되었음을 감지하고, 프론트엔드로 200 Warning 상태 및 수동 맵핑 요청 데이터를 반환한다.

## :gear: Technical & Non-Functional Constraints
- 성능: 맵핑 룰 로딩 및 정규식 검사는 p95 ≤ 300ms 이내에 완료되어야 함

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] 정규식 및 맵핑 로직에 대한 단위 테스트가 존재하는가?
- [ ] 사용자의 맵핑 룰이 정상적으로 DB에 저장/업데이트 되는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-CMD-02
- Blocks: TSK-CMD-04, TSK-TST-01
