# Enabling Scalable AI Computational Lithography with Physics-Inspired Models

## 메타데이터
- **저자**: Haoyu Yang, Haoxing Ren (NVIDIA)
- **연도**: 2023
- **게재지/학회**: Asia and South Pacific Design Automation Conference (ASPDAC 2023); SPIE DTCO and Computational Patterning II, Vol. 12495
- **DOI/URL**: https://doi.org/10.1145/3566097.3568361; https://doi.org/10.1117/12.2656025
- **인용수**: 40+

## 핵심 요약
NVIDIA 연구팀이 물리 기반 지식을 신경망 설계에 통합하여 확장 가능한 AI 기반 계산 리소그래피를 달성하는 방법론을 제시한 논문. 기존 CPU 기반 방법이 최신 칩 테이프아웃에 수천 CPU가 수일 동안 필요한 문제를 해결하기 위해, 리소그래피 도메인 지식을 직접 신경망 아키텍처에 통합한 물리 영감(physics-inspired) 접근법을 제안한다. Dual-band 구조, CFNO 등 이전 연구들을 통합한 확장 가능한 AI 리소그래피 프레임워크의 체계적 정리 논문이다.

## 주요 기여
- AI 기반 계산 리소그래피의 확장성 문제 해결 방법론 제시
- 리소그래피 도메인 지식을 신경망 아키텍처에 직접 통합
- UNet/ResNet 기반 접근법의 한계 분석 및 물리 영감 설계로 극복
- Dual-band 네트워크 + CFNO의 통합된 프레임워크 설명
- GPU/AI 가속 계산 리소그래피의 산업 배포 경로 제시

## 모델 아키텍처/수식
**기존 방법의 한계:**
```
기존 UNet/ResNet 기반:
- 도메인 지식 부재 → 일반화 성능 제한
- 고정 타일 크기 → 타일 이음새(stitch artifact) 문제
- 큰 모델 크기 → 메모리/속도 병목
```

**물리 영감 설계 원칙:**

**원칙 1: TCC 구조 모방 (Dual-band)**
리소그래피 TCC의 저주파/고주파 분리:
```
I(x) = I_low(x) + I_high(x)
      = Σ_{n=1}^{K_low} λₙ|φₙ⊗m|² + Σ_{n=K_low+1}^{K} λₙ|φₙ⊗m|²
```
신경망에서:
```
y = f_low(x) + f_high(x)
  = FNO(x)  +  Conv(x)
```

**원칙 2: 임의 크기 입력 (FNO)**
Fourier Neural Operator의 해상도 독립성:
```
L_FNO: x → IFFT(R_θ · FFT_truncated(x)) + Wx
```
FFT_truncated: 상위 K개 주파수 모드만 유지
→ 훈련 해상도 이상의 임의 크기 입력 처리 가능

**원칙 3: 물리 가이드 손실 (Litho Loss)**
```
L_physics = ||Litho(M) - L||² + λ₁·EPE + λ₂·PVBand
```
Litho: 미분 가능한 리소그래피 시뮬레이터 (TorchLitho)

**통합 프레임워크:**
```
[Lithography Simulation]
  CFNO Simulator: mask → wafer image
  ↕ (역방향 학습)
[Mask Optimization]
  CFNO Optimizer: layout → mask
  ↑
  LGST 자기 학습으로 반복 개선
```

**cuLitho 통합:**
- GPU 가속: H100 GPU 500개 = CPU 40,000개 동등
- 생성형 AI + cuLitho: 추가 2× 속도 향상
- TSMC 생산 배포

**산업 배포 결과:**
- 포토마스크 처리: 2주 → 하루 밤
- 전력 소비: 1/9 절감
- 공간: 1/8 절감

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 장기 발전 방향과 직접 관련된 논문. 현재 SKOPC가 CPU 기반 TorchLitho를 사용하는 것에서 GPU 가속 AI 모델로 전환하는 로드맵을 제시. NVIDIA cuLitho와의 통합 가능성 고려 시 이 논문의 프레임워크 참조 필요. 물리 영감 설계 원칙은 SKOPC의 GNN 아키텍처 고도화 방향을 제시한다.

## 참고문헌 (핵심)
- Yang, H. et al., "Generic lithography modeling with dual-band optics-inspired NNs," DAC 2022
- Yang, H. et al., "Large scale mask optimization via CFNO and LGST," arXiv:2207.04056 (2022)
- Li, Z. et al., "Fourier neural operator for parametric PDEs," ICLR 2021
- NVIDIA cuLitho: https://developer.nvidia.com/culitho

## 태그
`Model`, `OPC`, `AI`, `GPU`, `cuLitho`, `PhysicsInspired`, `Scalable`, `FNO`, `DualBand`, `CFNO`, `LGST`, `NVIDIA`, `TSMC`, `ProductionDeployment`, `ASPDAC`
