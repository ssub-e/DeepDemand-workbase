---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[UI/UX] TSK-FE-01: 엑셀 드래그 앤 드롭 업로더 및 맵핑 팝업"
labels: 'frontend, feature, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-FE-01] 드래그 앤 드롭 업로드 컴포넌트 구현
- 목적: TTV(Time To Value) 3분을 달성하기 위해, 고객이 가장 처음 마주하는 파일 업로드 인터페이스를 Zero-friction UX로 구성한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#411-제로-마찰-데이터-온보딩-f1`](#)

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] `react-dropzone` 패키지를 활용한 드래그 앤 드롭 존(Zone) 렌더링
- [ ] 파일 포맷(CSV/Excel 외) 오류 발생 시 `shadcn/ui` Toast(적색 경고창) 노출 이벤트 작성
- [ ] 서버로부터 `mapping_required: true` 응답 수신 시 컬럼 매핑(Mapping Wizard) 다이얼로그 팝업 렌더링 로직

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 프론트엔드 포맷 사전 차단
- Given: 사용자가 `.jpg` 이미지 파일을 드래그하여 업로더에 놓음
- When: `onDrop` 이벤트가 트리거됨
- Then: 서버에 요청을 보내지 않고 프론트엔드 레벨에서 즉시 "엑셀 또는 CSV 파일만 업로드 가능합니다" 토스트 알림을 띄운다.

## :gear: Technical & Non-Functional Constraints
- UX: 업로드 중(Uploading...) 상태일 때 버튼을 비활성화(Disabled) 하고 로딩 스피너를 보여주어야 한다.

## :checkered_flag: Definition of Done (DoD)
- [ ] Dropzone 컴포넌트가 디자인 시스템(Tailwind)에 맞게 렌더링되는가?
- [ ] 서버의 성공/에러 응답에 따라 각기 다른 Toast 메시지가 정상 노출되는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-MCK-01 (서버 목업 API 연결 필요)
- Blocks: TSK-FE-02
