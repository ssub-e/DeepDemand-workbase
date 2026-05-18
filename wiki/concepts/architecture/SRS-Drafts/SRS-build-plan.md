# SRS-V0.1 분할 작성 계획

## 목적
PRD v1.0 → SRS 변환 시 토큰 제한(64K)으로 인해 단일 패스 생성 불가.
아래 3단계로 분할 작성 후, 최종 SRS-V0.1.md에 병합한다.

## Source of Truth
- PRD: `wiki/concepts/business_strategy/saas-prd-v1.md`
- 표준: ISO/IEC/IEEE 29148:2018

## 분할 계획

| Step | 파일명 | SRS 섹션 | PRD 매핑 | 상태 |
|---|---|---|---|---|
| **Step 1** | `SRS-V0.1.md` (신규 생성) | §1 Introduction + §2 Stakeholders | PRD §1,2,7,9 → Purpose/Scope/Defs/Refs/Constraints + PRD §2 → Stakeholders | ✅ 완료 |
| **Step 2** | `SRS-V0.1.md` (append) | §3 System Context + §4 Requirements | PRD §3,4,5,6 → Functional/NFR + 시퀀스 다이어그램 | ✅ 완료 |
| **Step 3** | `SRS-V0.1.md` (append) | §5 Traceability + §6 Appendix | PRD §6,8 → API List/ERD/상세 시퀀스/검증계획 | ✅ 완료 |

## 10대 필수 수칙 체크리스트
- [x] 1) Story → REQ-FUNC Source 연결 ✅ (§4.1 모든 테이블에 Source 컬럼 명시)
- [x] 2) F1~F4 → 다수 REQ-FUNC 분해 ✅ (F1→6건, F2→5건, F3→2건, F4→1건 = 16건)
- [x] 3) 성능 수치 → NFR 이동 ✅ (REQ-NF-001~004 성능, 005~006 가용성)
- [x] 4) API → §3 + Appendix 이중 기재 ✅ (§3.3 API Overview + §6.1 상세 기재)
- [x] 5) 엔터티 → 표 구조화 ✅ (§6.2.2 엔터티 상세 정의 표)
- [x] 6) 시퀀스 → §3.4 + §6.3 이중 포함 ✅ (§3.4 핵심 1건 + §6.3 상세 2건)
- [x] 7) In/Out Scope → §1.2 명시 ✅ (SCOPE-IN 4건, SCOPE-OUT 3건)
- [x] 8) 리스크/가정 → Constraints/Assumptions 통합 ✅ (CON 6건, ASM 1건)
- [x] 9) References → REF-XX 형식 ✅ (REF-01~05)
- [x] 10) 모든 요구사항 → atomic ID 부여 ✅ (REQ-FUNC 16건 + REQ-NF 17건 = 33건)

## ✅ 작성 완료 (Rev 1.1 SaaS Pivot 업그레이드 완료)
- **최종 문서**: `SRS-V0.1.md` (660+ lines)
- **총 요구사항**: 40건 (FUNC 23 + NF 17)
- **총 Test Case**: 40건 (TC-F01~23 + TC-N01~17)
- **시퀀스 다이어그램**: 3건 (기상/트렌드 백그라운드 연동 포함)
- **검증 계획**: 2건 (EXP-01 Paired T-test, EXP-02 A/B Funnel)
- **피벗 정합성**: 100% (CSV 지원, 매핑 영속화, 온보딩 목적 선택, 3일 품절 경고, Quota 제한, Stripe/Toss API 및 빌링 ERD 반영 완료)
