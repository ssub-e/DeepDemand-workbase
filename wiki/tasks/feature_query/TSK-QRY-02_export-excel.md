---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-QRY-02: 발주 결과 포맷팅 및 Excel/CSV 1-Click 다운로드 스트림 변환 로직"
labels: 'feature, backend, priority:medium'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-QRY-02] 결과 엑셀 내보내기 (Export)
- 목적: 분석된 발주 추천 결과를 사용자의 실무 시스템(ERP)에 입력하기 용이하도록 Excel/CSV 파일 포맷으로 반환한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#412`](#)
- TASK 메타데이터: `§4.1.2 (REQ-019)`
- 선행 태스크: TSK-QRY-01

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] `GET /forecast/export` 엔드포인트 구현
- [ ] 조회된 결과 리스트 데이터를 DataFrame 기반으로 엑셀/CSV 포맷으로 변환(Pandas, OpenPyXL 등 활용)
- [ ] 대용량 파일 내보내기 시 메모리 고갈 방지를 위한 Streaming Response(스트림 청크) 전송 로직 구성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 결과 파일 다운로드
- Given: 예측 결과 데이터가 존재하는 테넌트
- When: `/forecast/export?format=xlsx` API를 호출함
- Then: HTTP 200 OK 응답과 함께 Content-Type `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet` 형태로 엑셀 파일이 다운로드됨.

## :gear: Technical & Non-Functional Constraints
- 성능: 수만 건의 데이터를 다운로드할 때 백엔드 메모리 점유율이 튀지 않게(Spike) File Streaming 방식을 적용할 것

## :checkered_flag: Definition of Done (DoD)
- [ ] 다운로드된 파일의 컬럼(SKU, 권장 발주량 등) 포맷이 올바른가?
- [ ] 대용량 다운로드 시 서버 리소스 모니터링 테스트를 통과했는가?
