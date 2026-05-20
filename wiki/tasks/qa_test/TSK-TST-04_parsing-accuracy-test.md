---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-TST-04: 엑셀/CSV 파싱 정확도 및 excel_mapping_rules 기반 컬럼 맵핑 성공률 단위 테스트"
labels: 'qa/test, priority:medium'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-TST-04] 파일 파싱 및 컬럼 매핑 단위 검증
- 목적: 사용자가 다양한 포맷으로 올리는 파일 데이터가 시스템의 요구 스키마(Mapping Rules)에 맞게 정확히 파싱되는지 검증한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#51`](#)
- TASK 메타데이터: `§5.1 (TC-F01)`
- 선행 태스크: TSK-CMD-04

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] 날짜 표기법, 숫자에 쉼표(,) 포함, 헤더 이름이 미세하게 다른 엣지 케이스용 더미 파일(Excel/CSV) 생성
- [ ] 파서 및 매핑 모듈에 더미 파일을 주입하여 리턴된 DataFrame 값 검증
- [ ] 필수 컬럼이 누락된 파일 주입 시 정확히 Error/Warning을 반환하는지 Assertion 작성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 다양한 포맷 데이터의 정규화 파싱
- Given: 숫자 천단위 콤마가 포함되고 '상품명'이 '제품이름'으로 표기된 엑셀 파일
- When: 파서 로직이 실행됨
- Then: 매핑 룰에 따라 '제품이름'이 `sku_name`으로 정상 매핑되고, 숫자 콤마가 제거된 Integer(정수) 타입으로 정확히 반환됨.

## :gear: Technical & Non-Functional Constraints
- 성능: 테스트 수행 시간이 전체 CI 파이프라인의 속도를 저하시키지 않도록 테스트용 파일 사이즈는 최소한(10 row 이하)으로 유지

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 엣지 케이스 테스트가 CI 상에서 성공하는가?
- [ ] 파서 모듈의 로직 커버리지가 90% 이상 도달했는가?
