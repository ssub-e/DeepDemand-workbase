---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-FE-04: 예측 근거 차트(14일 추이) 및 자연어 텍스트(Gemini 반환값) 우측 패널 렌더링"
labels: 'feature, frontend, ui/ux, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-FE-04] XAI 대시보드 (예측 근거 시각화 패널)
- 목적: AI 모델의 예측 결과에 대한 사용자의 불신을 해소하기 위해, 예측의 근거가 되는 과거 추이 차트와 LLM(Gemini) 기반 자연어 분석 리포트를 제공한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#413-결과-설명력xai-강화`](#)
- TASK 메타데이터: `§4.1.3 (REQ-013,020)`
- 선행 태스크: TSK-MCK-01, TSK-FE-03

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] 리스트 내 특정 SKU 클릭 시 우측 드로어(Drawer) 또는 별도의 상세 패널이 슬라이드인(Slide-in) 형태로 열리는 로직 구현
- [ ] 과거 14일 판매량 추이 및 향후 예측값을 시계열로 보여주는 Line/Bar Chart (Recharts, Chart.js 등 활용) 구현
- [ ] SHAP 밸류 및 Gemini API 기반으로 생성된 '자연어 분석 리포트' 텍스트를 렌더링하는 타이포그래피 영역 구현
- [ ] 로딩 상태(Skeleton UI) 및 에러 상태(Fallback UI) 처리

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 예측 근거 패널 오픈 및 데이터 확인
- Given: 발주 추천 리스트 화면이 열려 있음
- When: 사용자가 테이블에서 특정 SKU 행을 클릭함
- Then: 즉각적으로 우측에 상세 패널이 열리며, 과거 14일치 데이터 추이 차트와 "기온 하락 및 트렌드 검색량 증가로 수요 상승 예상" 등의 자연어 텍스트 리포트가 정상 표시됨.

Scenario 2: 데이터 로딩 및 에러 처리
- Given: 네트워크 지연으로 인해 XAI 근거 데이터 반환이 늦어지는 상황
- When: 사용자가 행을 클릭하여 패널을 염
- Then: 차트 및 텍스트 영역에 시각적으로 부드러운 Skeleton UI가 표시되며, 데이터 로드 실패 시 "데이터를 불러올 수 없습니다"라는 안내 문구와 재시도 버튼이 표시됨.

## :gear: Technical & Non-Functional Constraints
- 성능: 차트 렌더링 라이브러리 용량이 크므로 코드 스플리팅(Code Splitting) 적용하여 초기 로딩 속도 저하 방지
- 디자인: 패널 애니메이션(열림/닫힘)이 부자연스럽지 않도록 부드러운 전환 효과(Easing) 적용
- 호환성: 다양한 브라우저 해상도에서도 차트 툴팁(Tooltip)과 축(Axis) 텍스트가 짤리지 않게 반응형으로 개발

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] 차트 컴포넌트에 코드 스플리팅(Lazy Loading)이 적용되었는가?
- [ ] UI 레이아웃이 화면 크기 변화에 따라 유연하게 조절되는가?
- [ ] 컴포넌트 단위 테스트 및 엣지 케이스 처리(데이터가 null인 경우 등)가 완료되었는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-MCK-01 (Mock 데이터), TSK-FE-03 (리스트 뷰 완성)
- Blocks: None
