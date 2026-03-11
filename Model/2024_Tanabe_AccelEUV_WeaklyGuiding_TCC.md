# Accelerating Extreme Ultraviolet Lithography Simulation with Weakly Guiding Approximation and Source Position Dependent Transmission Cross Coefficient Formula

## 메타데이터
- **저자**: (Tanabe 그룹, 일본 / SPIE JMM 2024)
- **연도**: 2024
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 23, No. 1, 014201
- **DOI/URL**: https://doi.org/10.1117/1.JMM.23.1.014201

## 핵심 요약
EUV 리소그래피 시뮬레이션을 약한 안내 근사(weakly guiding approximation)와 소스 위치 의존 TCC(STCC) 공식으로 가속한다. 3D 도파관 모델의 결합 벡터 파동 방정식을 두 개의 스칼라 파동 방정식으로 분해하여 계산 시간을 줄이고, Abbe 이론보다 빠른 TCC 공식을 도입한다.

## 주요 기여
1. 약한 안내 근사(weakly guiding approximation)로 벡터 파동 방정식을 스칼라 방정식으로 분해
2. 소스 위치 의존 TCC(STCC) 공식 도입으로 Abbe 방식 대비 계산 가속
3. 학습 데이터 준비 시간 단축: 약한 안내 근사로 빠른 학습 데이터 생성
4. M3D 효과 포함 EUV 시뮬레이션의 속도-정확도 트레이드오프 최적화
5. CNN 학습 가속에 적용 가능한 빠른 데이터 생성 파이프라인

## 모델 수식/아키텍처
- **약한 안내 근사**:
  - 원래: ∇×∇×E - k²ε(r)E = 0 (두 편광 결합)
  - 근사: ∇²E_s + k²ε(r)E_s ≈ 0 (각 편광 분리, s = x,y)
- **STCC 공식**: TCC(f,g;f',g') = Σ_s J(s) · K*(f-s) · K(f'-s) (소스 위치 의존)
- 가속 효과: 벡터 FDTD 대비 계산 비용 ~1/2 감소
- Abbe vs. STCC: STCC가 Abbe 적분 대비 TCC 행렬 형태로 더 빠름

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC EUV 광학 엔진의 M3D 계산 가속을 위한 근사 방법 참조
- CNN 기반 EUV 시뮬레이터 학습 데이터 생성 파이프라인 가속에 적용
- `2024_Tanabe_CNN_EUV_M3D_Pretrain.md`와 같은 저자 그룹 — 물리 가속과 CNN의 결합
- TorchLitho 기반 미분 가능 EUV 시뮬레이션 엔진 구현 시 참조

## 태그
`Model`, `EUV`, `Simulation`, `WeaklyGuiding`, `TCC`, `STCC`, `Acceleration`, `M3D`, `Tanabe`, `JMM`, `SPIE`
