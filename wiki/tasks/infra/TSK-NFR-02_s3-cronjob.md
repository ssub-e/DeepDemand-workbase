---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-NFR-02: AWS S3 임시 파일 24시간 후 자동 파기 Cronjob 스크립트 작성 및 배포"
labels: 'infra, priority:medium'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-NFR-02] 임시 업로드 파일 자동 파기
- 목적: 사용자 원본 엑셀/CSV 데이터의 보안을 유지하고 S3 스토리지 비용을 최적화하기 위해 업로드 후 24시간이 지난 파일을 자동 삭제한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#423`](#)
- TASK 메타데이터: `§4.2.3 (REQ-008)`
- 선행 태스크: TSK-CMD-02

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] AWS S3 Bucket Lifecycle Policy 구성 또는 서버측 Cronjob 스크립트 작성
- [ ] 객체 생성 시간(Object Created At) 기준으로 24시간 초과 객체 필터링 로직 구현
- [ ] 파기 완료 후 Slack 또는 지정된 로깅 시스템에 파기 결과 알림 전송 로직 구성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 24시간 경과 객체 파기
- Given: S3 버킷에 업로드된 지 24시간이 지난 파일이 존재함
- When: 주기적인(Cron) 삭제 스크립트가 실행되거나 Lifecycle Policy가 트리거됨
- Then: 해당 파일이 S3에서 영구 삭제되며, 삭제 로그가 남음.

## :gear: Technical & Non-Functional Constraints
- 자동화: 인프라 종속성을 줄이기 위해 가급적 AWS S3 자체의 Lifecycle Configuration 사용 권장
- 보안: 파기 스크립트가 다른 백업 버킷이나 주요 데이터(DB 덤프 등)를 건드리지 않도록 권한(IAM) 최소화 원칙 준수

## :checkered_flag: Definition of Done (DoD)
- [ ] S3 Lifecycle Rule이 올바르게 적용되었는가?
- [ ] 실제 테스트 파일 업로드 후 지정된 시간 후 삭제되는지 모의(Mock) 검증 완료되었는가?
