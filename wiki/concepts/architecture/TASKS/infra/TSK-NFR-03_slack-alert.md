---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-NFR-03: FastAPI CPU/MEM 80% 이상 임계치 도달 시 Slack Webhook 알럿 발송 파이프라인 구축"
labels: 'infra, priority:medium'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-NFR-03] 시스템 리소스 모니터링 및 알럿
- 목적: 예측 연산으로 인해 백엔드(FastAPI) 인프라 리소스가 고갈될 경우, 즉시 인지하고 대응할 수 있도록 Slack 알림을 발송한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#425`](#)
- TASK 메타데이터: `§4.2.5 (REQ-010)`
- 선행 태스크: TSK-NFR-01

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] 서버(EC2/Render/Vercel) 리소스 상태 모니터링 에이전트(CloudWatch, Datadog 또는 로컬 데몬) 설정
- [ ] CPU 및 Memory 사용률이 80% 이상을 5분 이상 유지 시 알람을 트리거하는 임계치 규칙 설정
- [ ] Slack Incoming Webhook 연동 및 알람 메시지 템플릿(장애 위치, 현재 리소스 사용량) 구성

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 임계치 도달 시 알람 발송
- Given: 모니터링 에이전트가 실행 중인 백엔드 서버
- When: CPU 사용률이 80% 이상을 5분 지속함 (테스트를 위해 스트레스 테스트 툴 사용)
- Then: 지정된 Slack 채널로 현재 리소스 상태와 경고 메시지가 즉시 발송됨.

## :gear: Technical & Non-Functional Constraints
- 안정성: 모니터링 툴 자체가 서버 리소스를 과도하게 소모하지 않아야 함
- 편의성: 빈번한 알림으로 인한 피로도를 줄이기 위해 알림 쿨다운(Cooldown) 정책 적용

## :checkered_flag: Definition of Done (DoD)
- [ ] 임계치 도달 모의 테스트(Stress test)를 통해 Slack 알림이 정상 수신되었는가?
- [ ] 모니터링 대시보드(옵션)에서 현재 상태를 확인할 수 있는가?
