# Efficient Metrology for Edge Placement Error (EPE) Characterization Using Design for Inspection Methodology

## 메타데이터
- **저자**: Andrzej J. Strojwas, Dennis Ciplickas, Indranil De, Tomasz Brozek
- **연도**: 2022
- **게재지**: Proc. SPIE 12053, Metrology, Inspection, and Process Control XXXVI, 1205325
- **DOI/URL**: https://doi.org/10.1117/12.2614261

## 핵심 요약
설계 기반 검사(Design for Inspection) 방법론을 활용하여 EPE(Edge Placement Error) 특성화 계측을 효율화하는 방법론을 제안한 논문. 기존 스크라이브 라인(scribe line)에 제한된 Characterization Vehicle(CV) 배치의 한계를 극복하고, in-line 오버레이 계측과 최종 EPE 간의 상관관계 부족 문제를 해결하여 EPE 기반 수율 손실을 효과적으로 예방하는 프레임워크를 제시하였다.

## 주요 기여
1. **Design for Inspection 방법론**: EPE 계측을 위한 최적의 검사 패턴 설계 및 배치 방법론
2. **CV 배치 한계 극복**: 스크라이브 라인 제한 배치 대신 온칩(on-chip) EPE 계측 구조 설계
3. **전기적 미정렬 데이터와 수율 상관관계 실증**: 전기적 misalignment 계측 데이터와 실제 제품 수율 간의 강한 상관관계 입증
4. **in-line 오버레이-최종 EPE 불일치 발견**: in-line 오버레이 계측이 최종 EPE와 항상 상관관계를 갖지 않음을 실증
5. **허용 오차 초과 EPE와 수율 손실 연계**: 허용 한계를 초과하는 EPE가 수율 손실로 직결됨을 정량 분석

## 검증 방법론
- Design for Inspection 기반 CV 구조를 온칩에 배치하여 EPE 계측 데이터 수집
- in-line 오버레이 계측값과 웨이퍼 완료 후 전기적 EPE 측정값 비교
- 전기적 misalignment 데이터와 제품 수율 간의 통계적 상관관계 분석
- 허용 한계 초과 EPE 발생률과 수율 손실량 간의 정량적 관계 도출

## OPC 툴 구현 관련성
- SKOPC의 OPC 검증 모듈에서 EPE 계측 전략 설계 시 참조 (어떤 피처를 어디서 측정해야 수율 예측에 유효한지)
- `2021_Abramovitz_EPE_budget_margin_cooptimization_yield.md`와 함께 EPE 예산 분석-계측-수율 연계 프레임워크 구성
- 오버레이 계측만으로는 최종 EPE를 예측할 수 없다는 발견은 SKOPC 검증에서 CD+오버레이 통합 EPE 계산의 필요성 근거
- SKOPC Recipe Runner의 계측 계획(metrology plan) 기능 설계에 참조

## 태그
`Verification`, `SPIE`, `EPE`, `Metrology`, `Design for Inspection`, `Overlay`, `Yield`, `OPC`, `CD-SEM`
