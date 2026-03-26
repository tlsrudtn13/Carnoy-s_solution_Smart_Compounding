# (Modified) 카노이 솔루션 스마트 조제 및 DB 수집 시스템 for OMFS

> **(Modified) Carnoy Solution Smart Compounding & DB Collection System for OMFS**

[![GitHub Pages](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-blue?logo=github)](https://tlsrudtn13.github.io/Carnoy-s_solution_Smart_Compounding/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

구강악안면외과(OMFS) 수술 시 사용되는 카노이 용액(Carnoy's Solution)의 수동 조제 오차를 최소화하고, 임상 데이터를 체계적으로 수집·관리하기 위한 단일 HTML 기반 스마트 조제 보조 시스템입니다.

---

## 🔗 바로 사용하기

**→ [https://tlsrudtn13.github.io/Carnoy-s_solution_Smart_Compounding/](https://tlsrudtn13.github.io/Carnoy-s_solution_Smart_Compounding/)**

별도 설치 없이 모바일/PC 웹브라우저에서 바로 사용 가능합니다.

---

## 주요 기능

### ⚗️ 스마트 조제 (Smart Compounding)
- **중량법(Gravimetric) 기반** — 부피 눈금 대신 전자저울로 계량, ±3% 오차 범위 실시간 표시
- **영점 조절(Tare) 워크플로** — 성분별 순차 계량 지원
- **회생 모드(Salvage Mode)** — 한 성분이 목표량을 초과 투입되면 자동으로 전체 비율을 스케일업하여 폐기 없이 조제 완료 가능
- **Original / Modified Carnoy's 전환** — 클로로포름 포함/제외 배합 즉시 전환

### 📋 임상 DB 수집
- 환자번호, 수술일, 수술명, 예상/최종 진단명 입력
- 조제 완료 후 **localStorage 기반 DB에 자동 저장** (서버 불필요)
- 저장된 임상 정보는 조제 데이터와 **독립적으로 수정 가능** (수술 후 조직검사 결과 업데이트 등)
- **연구용 CSV 추출** — 전체 데이터를 Excel 호환 CSV로 내보내기

### 💾 임시 저장 (Auto-save Draft)
- 조제 중 페이지가 닫히거나 새로고침되어도 **모든 입력값 자동 저장**
- 재접속 시 복원 배너가 표시되며 클릭 한 번으로 복원

### 🌐 다국어 지원
- 한국어 / English 즉시 전환

---

## 배합 비율 (Formula)

| 성분 | Original Carnoy's | Modified Carnoy's |
|------|:---:|:---:|
| 무수 에탄올 (Absolute EtOH) | 6 mL (4.734 g) | 6 mL (4.734 g) |
| 클로로포름 (CHCl₃) | 3 mL (4.449 g) | — |
| 빙초산 (Glacial AcOH) | 1 mL (1.049 g) | 1 mL (1.049 g) |
| **염화제이철 FeCl₃** (고체 분말) | **1.000 g** | **1.000 g** |

> 허용 오차 ±3% 적용 (USP \<795\> ±10% 하한 대비 강화).
> FeCl₃는 액체 성분과 별도로 고체 분말을 직접 계량합니다.

**근거 문헌:** Voorsmit RACA et al. (1981). J Maxillofac Surg. 9(4):228–236. [PMID: 6172530](https://pubmed.ncbi.nlm.nih.gov/6172530/)

---

## 사용 방법

### 1단계 — 임상 정보 입력
페이지 상단 **임상 및 수술 정보** 섹션에 환자번호, 수술 날짜, 수술명, 예상 진단명을 입력합니다.
최종 진단명(조직검사 결과)은 저장 후 DB에서 수정 가능하므로 비워두어도 됩니다.

### 2단계 — 조제 설정
- **용액 종류**: Original(클로로포름 포함) 또는 Modified(클로로포름 제외) 선택
- **초기 목표 부피**: 기본 10 mL, 필요에 따라 변경 (배치 크기 배수로 자동 스케일)

### 3단계 — 성분 계량
성분 카드에 표시된 **목표 투입량(g)** 을 확인하며 전자저울로 계량합니다.

| 상태 | 표시 | 의미 |
|------|------|------|
| 🟢 녹색 | "완벽함" | 허용 범위 내 ±3% |
| 🔴 빨강 | "X.XXg 부족함" | 추가 투입 필요 |
| 🟡 황색 테두리 | 목표량 초과 감지 | 회생 모드 진입 |

#### 회생 모드 (Salvage Mode)
한 성분이 목표량의 103%를 초과하면 자동으로 회생 모드가 활성화됩니다.

1. 상단에 **노란 경고 배너** 표시
2. 각 성분 카드에 **영점 조절 후 추가량** 안내 박스가 열림
3. 저울을 0g으로 영점(Tare) 조절
4. 안내된 추가량만큼 더 계량 후 **적용** 버튼 클릭
5. 모든 성분 완료 후 **DB에 저장** — K값(비율계수)이 기록됨

### 4단계 — 저장 및 데이터 관리
- **DB에 저장** 버튼: 모든 성분이 목표량에 도달해야 활성화
- 저장된 기록은 하단 테이블에 자동 표시
- ✏️ 버튼 클릭 → 임상 정보(환자번호, 진단명 등) 인라인 수정
- 🗑️ 버튼 클릭 → 기록 삭제

### 5단계 — CSV 내보내기
우측 상단 **연구용 CSV 추출** 버튼으로 전체 DB를 Excel 호환 CSV 파일로 저장합니다.

---

## 데이터 저장 방식

| 항목 | 저장 위치 | 특징 |
|------|----------|------|
| 조제 기록 (DB) | `localStorage['carnoyDB']` | 브라우저 영구 저장 |
| 작성 중 임시 데이터 | `localStorage['carnoyDraft']` | 재접속 시 복원 가능 |

> ⚠️ **주의**: 브라우저 캐시/사이트 데이터 삭제 시 DB가 초기화됩니다. 중요한 데이터는 정기적으로 CSV로 내보내어 보관하세요.

---

## 개발 구조

```
/
├── index.html        # GitHub Pages 배포용 (gh-pages 브랜치)
├── maincode.html     # 개발 소스 (claude/review-manufacturing-html-U7xRW 브랜치)
├── LICENSE           # MIT License
└── README.md
```

- 순수 프론트엔드 단일 HTML 파일 (서버 불필요)
- [Tailwind CSS](https://tailwindcss.com/) (CDN), [Font Awesome](https://fontawesome.com/) (CDN), [Pretendard](https://github.com/orioncactus/pretendard) (CDN)

---

## 참고 문헌

1. Cutler EC, Zollinger R. *The use of sclerosing solutions in the treatment of cysts and fistulae.* **Am J Surg.** 1933;19(3):411–418.
2. Voorsmit RACA, Stoelinga PJW, Van Haelst UJGM. *The management of keratocysts.* **J Maxillofac Surg.** 1981;9(4):228–236. [PMID: 6172530](https://pubmed.ncbi.nlm.nih.gov/6172530/)
3. Dashow JE, et al. *Significantly Decreased Recurrence Rates in Keratocystic Odontogenic Tumor With Simple Enucleation and Curettage Using Carnoy's Versus Modified Carnoy's Solution.* **J Oral Maxillofac Surg.** 2015;73(11):2132–2135. [PMID: 26044601](https://pubmed.ncbi.nlm.nih.gov/26044601/)
4. Allen LV Jr. *Ansel's Pharmaceutical Dosage Forms and Drug Delivery Systems.* 11th ed. Wolters Kluwer; 2018.
5. ICH. *ICH Q8(R2) Pharmaceutical Development.* Step 4, August 2009.
6. USP General Chapter \<795\> *Pharmaceutical Compounding—Nonsterile Preparations.* Effective November 1, 2023.

---

## 만든이

**Kyung Su Shin** · JBUH, Oral & Maxillofacial Surgery (OMFS)
📧 [5848463@naver.com](mailto:5848463@naver.com)

---

## 면책 조항

이 소프트웨어는 연구 및 임상 참고 목적으로 제작되었습니다. 실제 조제는 자격을 갖춘 의료진의 판단과 기관 프로토콜에 따라 이루어져야 합니다. 본 도구 사용으로 인한 임상적 결과에 대해 제작자는 책임을 지지 않습니다.
