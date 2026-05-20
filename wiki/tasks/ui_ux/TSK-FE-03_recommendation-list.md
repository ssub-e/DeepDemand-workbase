---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-FE-03: 발주 추천 리스트 표출 및 3일 내 품절 임박(적색 신호등), 과재고 경고 아이콘 렌더링"
labels: 'feature, frontend, ui/ux, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-FE-03] 발주 추천 데이터 시각화 및 위험 경고 UI
- 목적: 사용자에게 SKU별 발주 추천 수량을 명확하게 제시하고, 긴급히 조치해야 할 품절/과재고 위험 상황을 직관적인 시각적 지표로 알려준다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#414-액션-추천-및-모니터링`](#)
- TASK 메타데이터: `§4.1.4 (REQ-014,021)`
- 선행 태스크: TSK-MCK-01

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] 발주 추천 리스트를 표출하는 Data Table 컴포넌트 구현 (정렬, 필터링, 페이지네이션 포함)
- [ ] API 반환값으로부터 추천 수량, 현재 재고, 예측 수요 데이터를 테이블 Row에 바인딩
- [ ] 재고 소진일(DOS) 계산 결과가 3일 이내인 경우 '적색 신호등/경고' 아이콘 렌더링 로직 추가
- [ ] 과재고 지표 초과(예: 권장 재고의 150% 이상) 시 '과재고 경고' 아이콘 렌더링 로직 추가
- [ ] 접근성을 고려한 아이콘 Hover Tooltip 구현

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: 긴급 품절 예상 SKU 시각적 표시
- Given: 백엔드 예측 결과 DOS(재고 소진일)가 2일인 SKU 데이터
- When: 발주 추천 리스트 화면이 렌더링됨
- Then: 해당 SKU Row의 상태 열에 명확한 적색 경고 아이콘과 함께 "3일 내 품절 예상" 툴팁이 제공되어야 함.

Scenario 2: 과재고 상태 표시
- Given: 현재 재고가 시스템 권장 적정 재고량보다 2배 이상 많은 SKU 데이터
- When: 발주 추천 리스트 화면이 렌더링됨
- Then: 해당 SKU Row에 잉여 재고를 경고하는 노란색(또는 파란색) 아이콘과 툴팁이 제공되어야 함.

## :gear: Technical & Non-Functional Constraints
- 성능: 최소 1,000개 이상의 행을 가진 테이블 렌더링 시 Virtualization(가상화) 기법을 적용하여 프레임 드랍(버벅임)을 방지
- 디자인: B2B SaaS 환경에 어울리는 정돈된 타이포그래피와 여백, 직관적인 시각적 계층 구조(Hierarchy) 적용
- 접근성: 색약 사용자(Color Blindness)를 위해 색상에만 의존하지 않고, 형태적 특성(아이콘 모양)과 텍스트를 반드시 병행 제공할 것

## :checkered_flag: Definition of Done (DoD)
- [ ] 모든 Acceptance Criteria를 충족하는가?
- [ ] Data Table 컴포넌트가 대량의 데이터에서도 60fps 스크롤 성능을 유지하는가?
- [ ] 반응형 웹 디자인이 적용되어 모바일 해상도에서 깨지지 않는가?
- [ ] UI 컴포넌트에 대한 Storybook 문서화 또는 단위 테스트가 완료되었는가?

## :construction: Dependencies & Blockers
- Depends on: TSK-MCK-01 (Mock 데이터 세팅)
- Blocks: None
