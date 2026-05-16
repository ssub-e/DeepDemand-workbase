# Timeline Log

위키에 수행된 모든 수집(Ingest), 생성, 점검(Lint) 기록입니다.

## [2026-04-22] 위키 인프라 초기화
- `CLAUDE.md` 스키마 및 컨벤션 문서 생성
- `index.md` 카탈로그 문서 생성
- `log.md` 타임라인 기록 문서 생성

## [2026-04-22] Ingest | 07_VPS_Final_for_PRD
- [source-vps.md](wiki/sources/source-vps.md) 요약본 생성
- [personas.md](wiki/entities/personas.md) 엔티티 추출
- [value-proposition.md](wiki/concepts/value-proposition.md) 컨셉 추출

## [2026-04-22] Ingest & Node Splitting | 비즈니스 분석 01~10번 대량 수집
- **Batch 1 (01, 02, 06번)**: 시장 구조(5 Forces), 경쟁 포지셔닝(Competitor), TAM/SAM/SOM 수치 분석 노드 분리
- **Batch 2 (03, 04, 05번)**: 가치사슬 벤치마킹, KSF(핵심 성공 요인), B2B 수요예측 최종 문제 정의서 노드 분리
- **Batch 3 (07, 08, 09, 10번)**: 극단적 분기형 CJM, 기회점수(AOS/DOS) 매트릭스, JTBD 심층 인터뷰 내용 추출 및 엔티티 연결
## [2026-04-22] Ingest & Node Splitting | SRS-V1.0.md
- **Tech Stack & Constraints**: SRS 기반 파이썬 단일 MVP 기술 스택(C-TEC) 정책 추출
- **API Spec**: Internal 및 External API 인터페이스 엔티티 분리
- `index.md` 구조에 C-TEC 및 API 스펙 노드 배치, Phase 2 (핵심 수집) 완료
- **Aggressive Structure**: PRD를 해체하여 다차원 폴더 노드로 생성
- [source-prd-v1.1.md](wiki/sources/specification/source-prd-v1.1.md) 요약 및 연결점(Bridge) 생성
- [erd-core-entities.md](wiki/entities/database/erd-core-entities.md) DB 엔티티 추출
- [tech-architecture.md](wiki/concepts/system_arch/tech-architecture.md) 기술 파이프라인 추출
- [adr-nfr.md](wiki/concepts/system_arch/adr-nfr.md) 아키텍처 제약 및 의사결정 추출
- [kpi-and-benchmarks.md](wiki/concepts/product_metrics/kpi-and-benchmarks.md) 핵심 지표 및 실험 설계 추출

## [2026-04-22] Task Mapping | GitHub Issues
- **Tasks Migration**: `e:/workspace/SRS-from-PRD/Tasks/issues/` 폴더에 있던 146개의 마크다운 태스크 문서를 `wiki/tasks/` 구조로 복사/분류 (DB, API, VIEW 등 prefix 기반)
- **Frontmatter Addition**: Obsidian 인식을 위한 `type: task` 및 `tags` 메타데이터 부여 완료
- **Task Indexing**: 전체 146개 태스크를 그룹핑한 `index-tasks.md` 생성 및 `wiki/index.md`에 연동. Phase 3 완료.

## [2026-05-16] Strategy Pivot | B2B to SaaS
- **SaaS Pivot Strategy**: 기존 B2B 중심 솔루션에서 범용 AI 수요예측 SaaS(PLG 모델)로의 전환을 위한 전략 문서 생성 ([saas-pivot-strategy.md](wiki/concepts/saas-pivot-strategy.md))
- **Index Update**: `index.md` 비즈니스 전략 섹션에 피벗 전략 노드 추가
- **SaaS Market Analysis**: 기존 B2B 5 Forces 프롬프트를 변환하여 SaaS 타겟 5 Forces 분석 문서 생성 ([saas-five-forces-market.md](wiki/concepts/business_strategy/saas-five-forces-market.md))
- **Prompt Library**: 신규 비즈니스 기획을 위한 범용 프롬프트 저장소 신설 및 5 Forces, 경쟁사 분석 프롬프트 추가 ([business-analysis-prompts.md](wiki/prompts/business-analysis-prompts.md))
- **SaaS Competitor Analysis**: 이커머스 플랫폼, 경량 OMS, BI 툴 등 3대 연관 시장을 도출하고 경쟁사 분석 리포트 생성 ([saas-competitor-analysis.md](wiki/concepts/business_strategy/saas-competitor-analysis.md))
- **SaaS Value Chain & KSF**: BoxHero, Inventory Planner 등 핵심 경쟁사를 선정하여 가치사슬 분석 수행 및 SaaS 피벗용 Top 5 KSF 도출. 범용 프롬프트 라이브러리에 해당 프롬프트 업데이트 완료.
- **SaaS Problem Definition**: SaaS 타겟 3대 시장 영역별로 고객이 겪는 핵심 문제를 정의한 문서 생성 ([saas-problem-definition.md](wiki/concepts/business_strategy/saas-problem-definition.md))
- **SaaS Market Sizing & Segment**: 시장 규모(TAM-SAM-SOM) 산정 및 고객 세분화(Market Segmentation) 분석 완료. 해당 프롬프트를 프롬프트 라이브러리에 6번째로 추가 ([saas-tam-sam-som.md](wiki/concepts/business_strategy/saas-tam-sam-som.md))
- **SaaS Persona Spectrum**: 시장 세분화 맵을 기반으로 핵심/확장/극단/비활성 페르소나 12명 도출 완료. 확장 페르소나의 논리적 근거(물류 소장, 도매업자 등 Value Chain 후방 인프라) 보강. 프롬프트 라이브러리에 7번째로 추가 ([saas-persona-spectrum.md](wiki/concepts/business_strategy/saas-persona-spectrum.md))
- **SaaS Primary Persona & CJM**: 4가지 기준(현실성, 차별성, 통찰성, 전략성)으로 최우선 페르소나(이지훈)를 도출하고, SaaS PLG 맥락에 맞춘 5단계 고객 여정 지도(CJM) 작성. 해당 프롬프트 2개를 라이브러리(8, 9번)에 추가 완료. ([saas-primary-persona.md](wiki/concepts/business_strategy/saas-primary-persona.md), [saas-cjm.md](wiki/concepts/business_strategy/saas-cjm.md))
- **SaaS AOS Matrix Analysis**: 페르소나 및 CJM에서 도출된 Pain Point들에 대해 조정형 기회점수(AOS)를 산출하고 사분면 매트릭스를 그려 MVP 최우선 개발 영역(Q1) 도출. 라이브러리에 프롬프트 10번으로 추가 완료. ([saas-aos-analysis.md](wiki/concepts/business_strategy/saas-aos-analysis.md))
- **SaaS DOS Matrix Analysis**: AOS 점수에 시장 규모(TAM%) 가중치를 곱해 실제 시장의 파급력을 구하는 DOS(발견된 기회점수) 방법론 적용. AOS-DOS 비교 매트릭스를 시각화하여 MVP 타겟 우선순위 교차 검증 완료. 프롬프트 11번 라이브러리 추가. ([saas-dos-analysis.md](wiki/concepts/business_strategy/saas-dos-analysis.md))
- **SaaS JTBD Interview Plan**: 최우선 페르소나의 '전환 사건'과 '4 Forces'를 검증하기 위한 6단계 JTBD 심층 인터뷰 계획 및 결과(가상) 요약 카드 생성. 라이브러리에 프롬프트 12번으로 추가. ([saas-jtbd-interview.md](wiki/concepts/business_strategy/saas-jtbd-interview.md))
- **SaaS Value Proposition Sheet**: 타겟 페르소나, JTBD 분석, AOS/DOS 매트릭스를 종합하여 솔루션의 핵심 차별적 가치를 정의한 한 장의 제안서(VPS) 작성 완료. 랜딩페이지 카피 포함. 프롬프트 13번 추가. ([saas-value-proposition-sheet.md](wiki/concepts/business_strategy/saas-value-proposition-sheet.md))
- **SaaS PRD v1.0**: PRD 및 PRD 품질 검증 프롬프트 2종(14, 15번)을 라이브러리에 추가. VPS를 기반으로 NFR(비기능 요구사항), 의존성, MoSCoW, On-call 모니터링 체계 등 엔지니어링 방어 디테일이 완벽히 포함된 고품질 PRD v1.0 문서 생성 완료. ([saas-prd-v1.md](wiki/concepts/business_strategy/saas-prd-v1.md))
