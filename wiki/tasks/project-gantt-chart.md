---
type: task-timeline
tags: [gantt, roadmap, project-management, timeline]
created: 2026-06-01
updated: 2026-06-01
---
# DeepDemand SaaS MVP - Project Gantt Chart & Roadmap

본 문서는 `index-tasks.md`에 정의된 30개 개발 태스크를 기반으로, 병렬 또는 독립적으로 진행할 수 있는 전체적인 개발 흐름과 태스크 간 의존성을 한눈에 보여주는 간트 차트(Gantt Chart) 및 일정 가이드라인입니다.

---

## 📊 1. DeepDemand SaaS MVP Gantt Chart (Mermaid)

다음 Mermaid 간트 차트는 각 태스크의 선-후행 관계 및 병렬 처리 가능한 워크스트림을 시각적으로 나타냅니다.

```mermaid
gantt
    title DeepDemand SaaS MVP 개발 일정 및 병렬 워크스트림
    dateFormat  YYYY-MM-DD
    axisFormat  %m-%d
    
    section Phase 1: Contract & Base Spec (Contract First)
    TSK-NFR-01: 스캐폴딩 및 배포 파이프라인 구축 :active, scaffold, 2026-06-01, 3d
    TSK-DB-01: DB 스키마 (Tenant/User)          :active, db1, 2026-06-01, 2d
    TSK-DB-02: DB 스키마 (Sales/Forecast)        :active, db2, after db1, 2d
    TSK-API-01: API 규약 (Auth)                :active, api1, 2026-06-01, 2d
    TSK-API-02: API 규약 (Forecast)            :active, api2, 2026-06-01, 3d
    TSK-API-03: API 규약 (Billing)             :active, api3, 2026-06-01, 2d
    TSK-MCK-01: Mocking API 구축               :active, mck1, after api2, 2d
    
    section Phase 2 (Parallel A): 백엔드 API & ML 파이프라인
    TSK-CMD-01: JWT 인증 미들웨어               :active, cmd1, after db1 api1, 3d
    TSK-CMD-09: Plan Quota 검증 미들웨어         :active, cmd9, after db1 api2, 3d
    TSK-CMD-02: 엑셀 파싱 및 기본 검증           :active, cmd2, after api2, 3d
    TSK-CMD-03: 컬럼 정규식 매핑                 :active, cmd3, after cmd2, 4d
    TSK-CMD-04: DB 이력 누적 적재                :active, cmd4, after cmd3 db2, 3d
    TSK-CMD-05: 비동기 예측 큐잉 트리거           :active, cmd5, after cmd4, 3d
    TSK-CMD-06: 날씨 및 트렌드 수집             :active, cmd6, after cmd5, 4d
    TSK-CMD-07: LightGBM & Fallback 분기       :active, cmd7, after cmd6, 4d
    TSK-CMD-08: SHAP 분석 및 Gemini 자연어 XAI    :active, cmd8, after cmd7, 4d
    TSK-QRY-01: 예측결과 폴링 및 리스트 조회       :active, qry1, after db2 api2, 3d
    TSK-QRY-02: 발주 파일 내보내기 (Download)     :active, qry2, after qry1, 2d
    
    section Phase 2 (Parallel B): 프론트엔드 UI/UX (Next.js)
    TSK-FE-01: FE 드롭존 업로더 & 매핑 Wizard   :active, fe1, after mck1, 5d
    TSK-FE-02: FE 온보딩 Wizard                :active, fe2, after mck1, 4d
    TSK-FE-03: FE 발주 추천 리스트 & 신호등 경고  :active, fe3, after mck1, 5d
    TSK-FE-04: FE XAI 스파이크 차트 및 패널      :active, fe4, after mck1, 5d

    section Phase 3: QA Validation & DevOps
    TSK-TST-01: QA 엑셀 업로드 유효성 검사 테스트 :active, tst1, after cmd3, 3d
    TSK-TST-04: QA 파서 정확도 및 맵핑 테스트     :active, tst4, after cmd4, 2d
    TSK-TST-05: QA Fallback 분기 테스트         :active, tst5, after cmd7, 2d
    TSK-TST-02: QA Free 요금제 한도 차단 테스트   :active, tst2, after cmd9, 2d
    TSK-TST-03: QA Multi-Tenant 격리성 테스트    :active, tst3, after cmd1 qry1, 3d
    TSK-NFR-02: S3 임시파일 24h TTL Cronjob     :active, nfr2, after cmd2, 2d
    TSK-NFR-03: Slack Webhook 알럿 파이프라인    :active, nfr3, after scaffold, 3d
    TSK-NFR-04: API 응답/예측 k6 부하 테스트      :active, nfr4, after qry1, 3d
```

---

## 🛠️ 2. 핵심 워크스트림 및 병렬 개발 전략 (Parallel Workstreams)

DeepDemand 개발 생태계는 **Contract-First(계약 우선)** 설계를 준수하므로, API 명세와 Mock 데이터 세팅이 완료되면 프론트엔드와 백엔드가 완전히 분리되어 병렬 개발을 진행할 수 있습니다.

### 1) 계약(Contract) 체결 단계: Phase 1 (초기 1~5일)
- 프론트엔드와 백엔드 개발자 모두가 모여 API 스키마(`TSK-API-01~03`)와 데이터베이스 스키마(`TSK-DB-01~02`)를 정의하고 확정합니다.
- 확정된 스펙을 기반으로 `TSK-MCK-01` Mocking API를 구성하면 프론트엔드는 백엔드 로직이 완료되기를 기다리지 않고 UI 개발에 돌입합니다.

### 2) 백엔드 핵심 파이프라인 (Backend Engine Stream)
백엔드 파이프라인은 크게 3개의 독립적인 경로로 나누어 병렬 구현이 가능합니다:
- **인증 및 보안 트랙**: `TSK-CMD-01` (JWT 미들웨어 구현) ➔ `TSK-CMD-09` (요금제 한도 필터 미들웨어 구현)
- **데이터 인입 및 전처리 트랙**: `TSK-CMD-02` (엑셀 업로드/파싱) ➔ `TSK-CMD-03` (컬럼 매핑) ➔ `TSK-CMD-04` (DB 저장)
- **비동기 ML 예측 트랙**: `TSK-CMD-05` (큐잉) ➔ `TSK-CMD-06` (외부 API 병합) ➔ `TSK-CMD-07` (모델 연산) ➔ `TSK-CMD-08` (SHAP/Gemini 리포팅)

### 3) 프론트엔드 UI 컴포넌트 개발 (Frontend Stream)
`TSK-MCK-01`에서 제공되는 Mock API를 활용하여 4가지 주요 기능 영역을 완전히 독립적이고 병렬로 개발할 수 있습니다:
- **드롭존 업로더 및 Wizard (`TSK-FE-01`)**
- **온보딩 레이아웃 분기 (`TSK-FE-02`)**
- **대시보드 추천 리스트 및 경고 위젯 (`TSK-FE-03`)**
- **XAI 추이 차트 및 자연어 리포트 패널 (`TSK-FE-04`)**

### 4) 자동 검증 및 데브옵스 (QA & DevOps Stream)
- **독립적 데브옵스**: `TSK-NFR-02` (S3 24h TTL) 및 `TSK-NFR-03` (Slack Webhook 알럿)은 뼈대 구축 및 파싱 기능 완료 직후 즉시 독립적으로 연동 및 배포할 수 있습니다.
- **인수조건(AC) 검증 테스트**: 백엔드 비즈니스 로직 및 조회 로직이 완성되는 대로 `TSK-TST-01~05` 단위/통합 테스트를 가동하여 요구사항 충족 여부를 확인합니다.
- **k6 부하 테스트 (`TSK-NFR-04`)**: `TSK-QRY-01` 조회 API 구축이 완료되는 즉시 백엔드 서버 부하(p95 ≤ 1500ms 만족 여부)를 테스트하여 최종 배포 안정성을 확보합니다.
