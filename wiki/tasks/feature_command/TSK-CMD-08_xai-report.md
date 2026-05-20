---
name: Feature Task
about: SRS 기반의 구체적인 개발 태스크 명세
title: "[Feature] TSK-CMD-08: 과재고/품절위험 지표 연산 및 Gemini API 활용 SHAP 예측 근거 자연어 리포트 생성 로직"
labels: 'feature, backend, priority:high'
assignees: ''
---

## :dart: Summary
- 기능명: [TSK-CMD-08] XAI(설명 가능한 AI) 근거 생성
- 목적: 단순 수치적 예측뿐만 아니라 사용자에게 왜 그런 예측이 나왔는지 설명(XAI)하기 위해 SHAP 밸류와 Gemini LLM을 결합하여 리포트를 생성한다.

## :link: References (Spec & Context)
> :bulb: AI Agent & Dev Note: 작업 시작 전 아래 문서를 반드시 먼저 Read/Evaluate 할 것.
- SRS 문서: [`/wiki/concepts/architecture/SRS-Drafts/SRS-V1.0.md#413`](#)
- TASK 메타데이터: `§4.1.3, §4.1.4`
- 선행 태스크: TSK-CMD-07

## :white_check_mark: Task Breakdown (실행 계획)
- [ ] `FORECAST_RESULT`와 현재 재고를 바탕으로 향후 14일 내 품절(DOS) 및 과재고 위험 지표 수학적 연산
- [ ] LightGBM 모델의 SHAP Value(피처 중요도) 추출 로직 적용
- [ ] 추출된 주요 피처 데이터를 Prompt 템플릿에 주입하여 Gemini API에 자연어 해설 요청
- [ ] 연산된 위험 지표와 Gemini 반환 텍스트를 `XAI_FACTOR` 테이블에 영속화

## :test_tube: Acceptance Criteria (BDD/GWT)
Scenario 1: SHAP 기반 Gemini 텍스트 생성
- Given: 기온 변수가 예측을 가장 크게 상승시킨(Positive SHAP) 예측 결과
- When: XAI 리포트 생성 로직이 실행됨
- Then: Gemini API가 "최근 기온 하락으로 인해 패딩의 수요가 평소 대비 20% 증가할 것으로 예측됩니다."와 같은 자연어 결과를 반환하고 DB에 저장됨.

## :gear: Technical & Non-Functional Constraints
- 비용/성능 최적화: 수천 개의 SKU에 대해 Gemini API를 개별 호출하면 비용 및 Rate Limit 문제가 발생하므로, 상위 Top N개 중요 SKU에만 자연어 리포트를 생성하도록 제한 규칙 추가

## :checkered_flag: Definition of Done (DoD)
- [ ] Gemini API 연동 모듈 및 프롬프트 템플릿이 작성되었는가?
- [ ] API Rate Limit 예외 처리가 반영되었는가?
