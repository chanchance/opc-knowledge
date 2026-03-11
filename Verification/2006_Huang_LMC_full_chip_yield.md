# Full-Chip Lithography Manufacturability Check for Yield Improvement

## 메타데이터
- **저자**: Yongfa Huang, Edward Tseng, Benjamin Szu-Min Lin, Chun Chi Yu, Chien-Ming Wang, Hua-Yu Liu
- **연도**: 2006
- **게재지**: Proc. SPIE 6156, Design and Process Integration for Microelectronic Manufacturing IV, 61560W
- **DOI/URL**: https://doi.org/10.1117/12.656401
- **인용수**: 다수 (UMC + Brion Technologies, LMC 분야 기준 논문)

## 핵심 요약
LMC(Lithography Manufacturability Check)는 전칩 웨이퍼 CD(Critical Dimension)를 10nm 이하 정확도로 예측하고 리소그래피 공정 윈도우를 분석하는 방법이다. FEM(Focus Exposure Matrix) 모델을 기반으로 단일 모델로 전체 포커스·노광 조건 범위를 시뮬레이션할 수 있으며, MEEF 체크와 함께 공정 취약점을 포착한다. 실제 설계에 적용하여 전칩 공정 윈도우 분석 및 수율 향상에 대한 이점을 실증한다.

## 주요 기여
1. FEM 모델 기반 전칩 LMC — 포커스·노광 조건 전체를 단일 모델로 시뮬레이션
2. CD 예측 정확도 10nm 이하 달성 — 전칩 레벨 수율 예측 가능한 수준
3. MEEF 체크를 LMC와 통합하여 공정 취약 패턴을 체계적으로 포착
4. UMC 양산 환경 실제 설계 데이터로 실증 — 산업적 실용성 검증

## 검증 방법론
- **FEM(Focus Exposure Matrix) 모델**:
  - 포커스 변동(ΔF)과 노광량 변동(ΔE)의 2D 행렬로 공정 조건 공간 망라
  - 단일 모델로 전체 공정 윈도우 시뮬레이션 — 다중 모델 필요 없음
- **전칩 CD 예측**: 각 패턴 세그먼트에서 FEM 모델 기반 CD 시뮬레이션 → 설계 타겟 대비 오차 계산
- **MEEF 체크**: 전칩 MEEF 분포 분석으로 고-MEEF 취약 패턴 자동 식별
- **공정 윈도우 분석**: DOF(Depth of Focus), EL(Exposure Latitude) 마진 전칩 맵핑
- **평가 지표**:
  - CD 예측 정확도: < 10nm (실측 vs. 시뮬레이션)
  - 핫스팟 포착률 (공정 윈도우 마진 부족 패턴 검출률)

## 검증 지표
- EPE 허용 범위: CD 오차 < 10nm (전칩 레벨)
- 시뮬레이터: Brion Technologies LMC 엔진 (FEM 모델 기반)
- 커버리지: 전칩 레이아웃 전체 (UMC 실제 칩 데이터베이스)

## OPC 툴 구현 관련성
- **전칩 CD 예측 기반 OPC 검증 구현 참조**: `VerificationEngine`의 전칩 공정 윈도우 분석 모듈에서 FEM 모델 기반 CD 예측 및 MEEF 체크를 통합하는 설계에 직접 활용
- FEM 모델은 `LithoEngine`의 공정 조건 확장(포커스·노광 변동) 시뮬레이션 구조 구현의 기반
- 전칩 MEEF 분포 맵핑으로 OPC 검증 결과를 수율 추정과 연계하는 아키텍처 근거
- CD 예측 정확도 10nm 이하는 90nm~65nm 노드 OPC 검증 정확도 목표 기준으로 활용 가능

## 참고문헌
- SPIE Design and Process Integration for Microelectronic Manufacturing IV 2006, Vol. 6156
- United Microelectronics Corp. (UMC) + Brion Technologies 협력 연구

## 태그
`Verification`, `SPIE`, `LMC`, `FullChip`, `FEM`, `MEEF`, `ProcessWindow`, `CDPrediction`, `YieldImprovement`, `OPCVerification`
