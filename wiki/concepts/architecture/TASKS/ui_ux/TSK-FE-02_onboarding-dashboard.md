---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-FE-02: 최초 온보딩 목적(forecast_purpose) 선택 및 목적별 대시보드 레이아웃 분기 렌더링"
labels: 'feature, frontend, ui/ux, priority:medium'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-FE-02] 온보딩 및 맞춤형 대시보드 렌더링
- 목적: 사용자의 주요 서비스 이용 목적을 파악하고 이에 최적화된 UI/UX 레이아웃을 제공하여 사용자 만족도를 극대화한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#411-데이터-수집-및-전처리-ingestion`](#)
- TASK 메타데이터: `§4.1.1 (REQ-022)`
- 선행 태스크: TSK-MCK-01

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] 온보딩 모달/페이지 퍼블리싱 (이용 목적 선택지 UI 구현)
- [ ] 사용자가 선택한 목적(`forecast_purpose`)을 User Context 또는 상태 관리 스토어(Zustand, Context API 등)에 영속성 있게 저장
- [ ] 저장된 상태 값에 따라 메인 대시보드의 위젯 구성 및 레이아웃을 다르게 렌더링하는 조건부 라우팅/컴포넌트 로직 구현
- [ ] 모바일/태블릿 반응형 대응 디자인 적용

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 온보딩 목적 선택 및 대시보드 진입
- Given: 서비스에 최초 로그인한 사용자
- When: 온보딩 화면에서 '적정 재고 관리' 목적을 선택하고 완료 버튼을 클릭함
- Then: 메인 대시보드 렌더링 시, 재고 관리 중심의 위젯(과재고 경고, 적정 재고 알림 등)이 최상단에 강조 배치되어야 함.

Scenario 2: 온보딩 목적 재선택(설정 변경)
- Given: 이미 온보딩을 마친 사용자
- When: 환경 설정(Settings) 메뉴에서 이용 목적을 '매출 극대화'로 변경함
- Then: 대시보드 레이아웃이 즉각적으로 매출 추이 및 프로모션 예측 중심의 위젯으로 실시간 재구성됨.

## :gear: Technical & Non-Functional Constraints
- 호환성: React Context 또는 전역 상태 관리 라이브러리(Zustand 등)의 활용하여 불필요한 리렌더링 방지
- 사용성: 초기 온보딩 스텝은 간결해야 하며 3번 이상의 클릭을 요구하지 않아야 함
- 성능: 온보딩 완료 시 화면 전환 애니메이션을 60fps로 부드럽게 제공할 것

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] 브라우저 환경에서 경고/에러 로그가 출력되지 않는가?
- [ ] 반응형 웹 디자인이 모바일 기기에서도 정상 작동하는가?
- [ ] 컴포넌트 단위 테스트(Jest/React Testing Library)가 통과하는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-MCK-01 (UI 개발용 Mock API)
- Blocks: None
