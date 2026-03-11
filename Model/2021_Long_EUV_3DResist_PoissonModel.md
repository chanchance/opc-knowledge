# Three-Dimensional Modeling of EUV Photoresist Using the Multivariate Poisson Propagation Model

## 메타데이터
- **저자**: Luke T. Long, Andrew R. Neureuther, Patrick P. Naulleau
- **연도**: 2021
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 20, No. 3, 034601
- **DOI/URL**: https://doi.org/10.1117/1.JMM.20.3.034601

## 핵심 요약
다변량 포아송 전파 모델(multivariate Poisson propagation model)의 3D 버전을 개발하여 EUV 레지스트의 확률론적 시뮬레이션을 수행한다. 다양한 z-blur 조건에서 10⁵개의 비아(via)를 시뮬레이션하여 산 확산(acid diffusion)의 역할을 탐구한다.

## 주요 기여
1. 다변량 포아송 전파 모델(MPPM)의 3D 버전 개발 및 EUV 레지스트 적용
2. 10⁵개 비아 시뮬레이션으로 통계적으로 유의미한 확률론적 거동 분석
3. z-blur(Z 방향 산 확산) 조건이 비아 패터닝 수율에 미치는 영향 정량화
4. 3D 레지스트 프로파일과 EUV 확률론적 실패율의 상관관계 도출
5. Neureuther-Naulleau 그룹의 EUV 확률론적 레지스트 모델링 연구

## 모델 수식/아키텍처
- **다변량 포아송 전파 모델(MPPM)**:
  - 광자 흡수: N_photon(x,y,z) ~ Poisson(λ(x,y,z))
  - 산 생성: N_acid ~ Poisson(η · N_photon) (η: 산 생성 효율)
  - 3D 산 확산: ∂C/∂t = D_x·∂²C/∂x² + D_y·∂²C/∂y² + D_z·∂²C/∂z²
  - z-blur: Z방향 산 확산이 3D 레지스트 프로파일 결정
- 현상 모델: 국소 탈보호 분율 → 3D 현상 속도 → 비아 프로파일
- 통계 분석: 10⁵ 비아 시뮬레이션 → 실패율, CD 분포, 브리징/끊어짐 통계

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC EUV 레지스트 모델에 3D 확률론적 효과 추가 시 핵심 참조
- 비아/컨택 레이어 EUV OPC에서 확률론적 실패율 예측에 직접 활용
- `2014_Neureuther_EUV_OPC_Requirements.md` (기존)와 같은 Neureuther 그룹 연구
- `2023_Gillijns_CompactStochastic_OPC_Application.md`의 엄밀 모델 기반 제공

## 태그
`Model`, `Resist`, `EUV`, `Stochastic`, `3D`, `Poisson`, `AcidDiffusion`, `Via`, `Neureuther`, `JMM`, `SPIE`
