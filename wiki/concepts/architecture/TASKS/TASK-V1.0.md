# DeepDemand SaaS MVP - Github Project Task Breakdown (V1.0)

> 본 문서는 `SRS-V1.0.md`의 요구사항을 바탕으로, **Data & Contract First ➔ Read/Write Isolation ➔ Test Validation** 추출 전략에 따라 작성된 최종 개발 태스크 명세서입니다. 깃허브 프로젝트(Github Projects) 또는 Jira에 일괄 등록(Import)하여 스프린트 계획을 수립하는 데 최적화되어 있습니다.

---

## 📋 Task List (Markdown Table)

| Task ID | Epic (도메인) | Feature (기능명) | 관련 SRS 섹션 | 선행 태스크 (Dependencies) | 복잡도 (H/M/L) |
|---|---|---|---|---|---|
| **TSK-NFR-01** | Infra | Next.js, FastAPI 스캐폴딩 및 Vercel/Render 초기 자동 배포 파이프라인 구축 | §3.2, §3.4 | None | M |
| **TSK-DB-01** | Data Model | [DB] `TENANT`, `USER`, `UPLOAD_LOG` 테이블 스키마 및 외래키(Supabase SQL) 작성 | §6.2.2 | None | L |
| **TSK-DB-02** | Data Model | [DB] `DAILY_SALES_HISTORY`, `FORECAST_RESULT`, `SKU_METRICS`, `XAI_FACTOR` 스키마 작성 | §6.2.2 | TSK-DB-01 | L |
| **TSK-API-01** | API Spec | [API Spec] Auth 도메인 (로그인) Request/Response DTO 및 예외 코드 정의 | §6.1 (API-01) | None | L |
| **TSK-API-02** | API Spec | [API Spec] Forecast 도메인 (업로드/트리거/폴링/조회) DTO 및 에러 코드 정의 | §6.1 (API-02~06) | None | M |
| **TSK-API-03** | API Spec | [API Spec] Billing 도메인 (결제 세션/웹훅) DTO 규약 정의 | §6.1 (API-07~08) | None | L |
| **TSK-MCK-01** | Mock Data | [Mock] 프론트엔드 UI 개발용 발주 추천 결과 및 403 에러 Mocking API 세팅 | §6.1 (API-05) | TSK-API-02 | L |
| **TSK-CMD-01** | Auth | [Feature/Command] JWT 기반 로그인 인증 로직 및 Tenant ID 검증 미들웨어 구현 | §4.1.5 (REQ-015) | TSK-DB-01, TSK-API-01 | M |
| **TSK-CMD-02** | Ingestion | [Feature/Command] 업로드 파일(.xlsx/.csv) Pandas 파싱 및 용량/포맷(10MB 이하) 검증 로직 | §4.1.1 (REQ-001,003)| TSK-API-02 | M |
| **TSK-CMD-03** | Ingestion | [Feature/Command] 필수 컬럼 정규식 매핑 검증 및 `excel_mapping_rules` 영속화 분기 처리 로직 | §4.1.1 (REQ-004,005)| TSK-CMD-02 | H |
| **TSK-CMD-04** | Ingestion | [Feature/Command] 파싱 성공 데이터 `DAILY_SALES_HISTORY` 및 `UPLOAD_LOG` 누적 인서트(Append) 로직 | §4.1.1 (REQ-016,017)| TSK-CMD-03, TSK-DB-02 | M |
| **TSK-CMD-05** | Forecast | [Feature/Command] 예측 시작 트리거 및 `FastAPI BackgroundTasks` 큐 할당 비즈니스 로직 | §4.1.2 (REQ-007) | TSK-CMD-04 | M |
| **TSK-CMD-06** | Forecast | [Feature/Command] 기상청 단기예보 및 네이버 DataLab API 백그라운드 데이터 병합 수집 로직 | §4.1.2 (REQ-018) | TSK-CMD-05 | H |
| **TSK-CMD-07** | Forecast | [Feature/Command] 이력 기간 판별(14일) 기반 LightGBM 연산 및 Rule-based 안전재고 Fallback 분기 로직 | §4.1.2 (REQ-008,009)| TSK-CMD-06 | H |
| **TSK-CMD-08** | Forecast | [Feature/Command] 과재고/품절위험 지표 연산 및 Gemini API 활용 SHAP 예측 근거 자연어 리포트 생성 로직 | §4.1.3, §4.1.4 | TSK-CMD-07 | H |
| **TSK-CMD-09** | Monetization | [Feature/Command] 테넌트 Plan 기반 SKU 예측 한도(Quota) 검증 및 차단(403) 미들웨어 구현 | §4.1.2 (REQ-023) | TSK-DB-01, TSK-API-02 | M |
| **TSK-QRY-01** | Forecast | [Feature/Query] `GET /status` 폴링 응답 및 SKU별 발주 추천 리스트, 신뢰도/품절경고 지표 조회 로직 | §4.1.2 (REQ-010,011)| TSK-DB-02, TSK-API-02 | M |
| **TSK-QRY-02** | Forecast | [Feature/Query] 발주 결과 포맷팅 및 Excel/CSV 1-Click 다운로드 스트림 변환 로직 | §4.1.2 (REQ-019) | TSK-QRY-01 | M |
| **TSK-FE-01** | UI/UX | [UI] 엑셀/CSV 드래그 앤 드롭 업로더, 오류 토스트, 매핑 Wizard 팝업 렌더링 (Next.js) | §4.1.1 (REQ-001~004)| TSK-MCK-01 | M |
| **TSK-FE-02** | UI/UX | [UI] 최초 온보딩 목적(`forecast_purpose`) 선택 및 목적별 대시보드 레이아웃 분기 렌더링 | §4.1.1 (REQ-022) | TSK-MCK-01 | M |
| **TSK-FE-03** | UI/UX | [UI] 발주 추천 리스트 표출 및 3일 내 품절 임박(적색 신호등), 과재고 경고 아이콘 렌더링 | §4.1.4 (REQ-014,021)| TSK-MCK-01 | M |
| **TSK-FE-04** | UI/UX | [UI] 예측 근거 차트(14일 추이) 및 자연어 텍스트(Gemini 반환값) 우측 패널 렌더링 | §4.1.3 (REQ-013,020)| TSK-MCK-01 | M |
| **TSK-TST-01** | QA & Test | [Test] 미지원 파일 업로드 시 1000ms 내 400 에러 반환(AC) 및 필수 컬럼 누락 200 Warning 단위 테스트 | §5.1 (TC-F03,F04) | TSK-CMD-03 | L |
| **TSK-TST-02** | QA & Test | [Test] Free 유저 1 SKU 초과 예측 트리거 시 403 Forbidden 차단(AC) 단위 테스트 | §5.1 (TC-F23) | TSK-CMD-09 | L |
| **TSK-TST-03** | QA & Test | [Test] 타 테넌트 JWT 토큰으로 `GET /forecast` 강제 접근 시 데이터 격리 차단(AC) 통합 테스트 | §5.1 (TC-F15) | TSK-CMD-01, TSK-QRY-01| M |
| **TSK-TST-04** | QA & Test | [Test] 엑셀/CSV 파싱 정확도 및 `excel_mapping_rules` 기반 컬럼 맵핑 성공률 단위 테스트 | §5.1 (TC-F01) | TSK-CMD-04 | M |
| **TSK-TST-05** | QA & Test | [Test] 이력 데이터 14일 미만 시 Rule-based Fallback 분기(AC) 정상 작동 여부 단위 테스트 | §5.1 (TC-F09) | TSK-CMD-07 | M |
| **TSK-NFR-02** | Infra | [Infra] AWS S3 임시 파일 24시간 후 자동 파기 Cronjob 스크립트 작성 및 배포 | §4.2.3 (REQ-008) | TSK-CMD-02 | L |
| **TSK-NFR-03** | Infra | [Infra] FastAPI CPU/MEM 80% 이상 임계치 도달 시 Slack Webhook 알럿 발송 파이프라인 구축 | §4.2.5 (REQ-010) | TSK-NFR-01 | M |
| **TSK-NFR-04** | QA & Test | [Infra] API 응답시간(p95 ≤ 1500ms) 및 예측 연산 지연시간 검증을 위한 k6 부하 테스트 스크립트 작성 | §5.2 (REQ-NF-01~04)| TSK-QRY-01 | M |

---

### 💡 Workflow Execution Guide (에이전트 오케스트레이션 가이드)
본 리스트를 활용해 Vibe Coding을 진행할 때, AI 에이전트(Cursor, Cline 등)에게 다음과 같은 순서로 지시하십시오.

1. ** Phase 1 (계약 체결)**: `TSK-DB-01`, `TSK-API-01`, `TSK-MCK-01` 등 "데이터 명세" 태스크를 가장 먼저 지시합니다. 이 과정이 끝나면 프론트엔드와 백엔드가 참조할 뼈대가 굳어집니다.
2. ** Phase 2 (프론트/백엔드 병렬 개발)**: `TSK-FE-01~04`(프론트엔드 UI 컴포넌트) 작업과 `TSK-CMD-01~09`(백엔드 상태 변경 API) 작업을 동시에 별개의 에이전트에게 지시해도 무방합니다. (이미 Mock 데이터와 DTO가 확정되었기 때문입니다.)
3. ** Phase 3 (자동 검증)**: 비즈니스 로직 작성 후 `TSK-TST-01~03` 태스크를 지시하여 에이전트 스스로 작성한 로직이 AC(인수조건)를 만족하는지 유닛 테스트로 검증하도록 만듭니다.
