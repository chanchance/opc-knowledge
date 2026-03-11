# Physics-informed Neural Networks and Neural Operators for EUV Electromagnetic Wave Diffraction from a Lithography Mask

## 메타데이터
- **저자**: Vasiliy A. Es'kin, Egor V. Ivanov
- **연도**: 2025
- **게재지/학회**: arXiv preprint (math.NA — 수치 해석, AI, 계산 물리학)
- **DOI/URL**: https://arxiv.org/abs/2507.04153
- **인용수**: 미확인 (2025년 7월 최신 논문)

## 핵심 요약
EUV 리소그래피 마스크에서의 전자기파(EM) 회절 문제를 풀기 위한 물리 정보 신경망(PINN)과 신경 연산자(Neural Operator) 접근법을 제안한다. 핵심 기여는 도파관(waveguide) 방법의 가장 계산 집약적인 부분을 신경망으로 대체한 하이브리드 WGNO(Waveguide Neural Operator)다. 실제적인 2D 및 3D 마스크 형상에서의 수치 실험을 통해 최신 정확도와 추론 시간을 달성하며, 마스크 설계 워크플로우의 OPC 설계 주기를 크게 가속화할 수 있는 유망한 도구다.

## 주요 기여
- **WGNO 하이브리드 방법**: 도파관 물리 방법과 신경망 가속을 결합한 하이브리드 Waveguide Neural Operator
- **EUV 마스크 3D 시뮬레이션**: 실제 2D 및 3D 마스크 형상에서의 EUV 전자기파 회절 시뮬레이션
- **최신 정확도 달성**: 전통적인 방법 대비 정확도와 추론 시간 모두에서 최신 성능 달성
- **OPC 설계 주기 가속**: EUV 마스크 설계 워크플로우의 전체 가속으로 OPC 턴어라운드 시간 단축
- **짧은 학습 기간**: 높은 정확도 달성에 매우 짧은 학습 기간만 요구

## 검증 방법론
- **2D/3D 마스크 수치 실험**: 실제적인 2D 및 3D EUV 마스크 형상에서 WGNO 성능 검증
- **전통적 솔버 비교**: 리고러스 전자기 솔버(FDTD/RCWA) 대비 정확도 및 속도 비교
- **다른 신경 연산자 비교**: DeepONet, Fourier Neural Operator 등 다른 신경 연산자와 비교
- **PINN 단독 비교**: WGNO와 순수 PINN 방법 성능 비교
- **현실적 마스크 패턴**: 실제 반도체 제조에 사용되는 마스크 패턴으로 검증

## 검증 지표
- **EPE 허용 범위**: 마스크 3D 효과(M3D)로 인한 EPE 예측 정확도
- **정확도**: 리고러스 EM 솔버 대비 근장(near-field) 및 원장(far-field) 계산 정확도
- **추론 속도**: 훈련 후 단일 마스크 패턴의 EM 시뮬레이션 추론 시간
- **사용 시뮬레이터**: WGNO (자체 개발), 비교: RCWA/FDTD 등 리고러스 EM 솔버
- **검증 커버리지**: 2D 및 3D EUV 마스크 형상, 다양한 마스크 재료 및 형상

## OPC 툴 구현 관련성
SKOPC의 EUV OPC 및 마스크 3D 효과 보정 모듈에 직접 활용 가능:
1. **마스크 3D 효과 모델링**: WGNO를 SKOPC의 EUV OPC에서 마스크 3D 효과(M3D) 보정에 활용
2. **빠른 EM 시뮬레이션**: 리고러스 EM 솔버를 WGNO로 대체하여 OPC 검증 속도 향상
3. **EUV OPC 정확도 향상**: 3D 마스크 효과를 정확히 모델링하여 EUV OPC의 EPE 감소
4. **EUV 마스크 설계 가속**: 마스크 흡수체 형상 최적화 사이클 단축
5. **고NA EUV 지원**: 0.55 NA 고NA EUV 리소그래피의 강화된 3D 마스크 효과 처리

## 참고문헌 (핵심)
- RCWA(Rigorous Coupled Wave Analysis) 관련 EUV 마스크 시뮬레이션 기존 연구
- FDTD(Finite Difference Time Domain) 방법론 관련 참고문헌
- Li et al. (2021) - Fourier Neural Operator (FNO): 신경 연산자 기초
- Lu et al. (2021) - DeepONet: 딥 연산자 네트워크
- EUV 마스크 3D 효과(M3D) 관련 SPIE 리소그래피 선행 연구

## 태그
`Verification`, `OPC`, `EUV`, `Mask 3D Effect`, `M3D`, `Electromagnetic Simulation`, `Physics-informed`, `Neural Operator`, `WGNO`, `Waveguide Method`, `2025`, `3D Mask`, `High-NA EUV`
