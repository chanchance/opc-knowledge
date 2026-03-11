# Inverse Lithography Physics-informed Deep Neural Level Set for Mask Optimization

## 메타데이터
- **저자**: Xu Ma, Hao Hao, 외
- **연도**: 2023
- **게재지/학회**: Applied Optics, Vol. 62, No. 33, pp. 8769 (November 2023); arXiv:2308.12299
- **DOI/URL**: https://arxiv.org/abs/2308.12299; https://opg.optica.org/ao/abstract.cfm?uri=ao-62-33-8769
- **인용수**: 30+

## 핵심 요약
역리소그래피 물리 정보를 통합한 깊은 신경망 레벨셋(ILDLS: Inverse Lithography physics-informed Deep neural Level Set) 마스크 최적화 방법을 제안한 논문. 딥러닝(UNet) 기반 초기 마스크 예측에 레벨셋 기반 ILT 보정 레이어를 추가하는 2단계 학습 전략을 사용한다. 순수 딥러닝 방법과 순수 ILT 방법의 장점을 결합하여, ILT 대비 수 오더(order of magnitude) 빠른 계산 속도와 순수 딥러닝 대비 우수한 패턴 충실도 및 공정 윈도우를 달성한다.

## 주요 기여
- 딥러닝과 레벨셋 ILT를 단일 프레임워크로 통합하는 ILDLS 방법 제안
- 2단계 학습: UNet 사전학습 → ILT 보정 레이어 통합 학습
- 리소그래피 물리 지식을 딥러닝 학습에 명시적으로 내재화
- ILT 대비 수 오더 계산 시간 단축
- 공정 윈도우(PW) 개선: 초점/노광량 변동에 대한 견고성 향상
- Applied Optics에 게재된 학술 검증 결과

## 모델 아키텍처/수식
**전체 ILDLS 파이프라인:**
```
Layout → [Step 1: Pre-trained UNet] → Initial Mask M₀
       → [Step 2: ILT Correction Layer] → Corrected Mask M*
```

**Step 1: UNet 사전학습**
- 입력: 타겟 레이아웃 (binary, 512×512)
- 출력: 초기 마스크 추정치 M₀
- 학습 데이터: ILT로 최적화된 (layout, mask) 쌍
- 손실: L_pre = ||M₀ - M_ILT||²

**Step 2: ILT 보정 레이어 (레벨셋 기반)**
레벨셋 함수 φ를 이용한 마스크 표현:
```
M(x) = H(φ(x))    (H: Heaviside 함수)
```

레벨셋 ILT 최적화:
```
∂φ/∂t = -δ(φ) · ∂E/∂M · |∇φ|
```
여기서:
- E: 리소그래피 손실 함수
- δ(φ): Dirac delta (경계에서만 업데이트)
- ∂E/∂M: 마스크에 대한 리소그래피 손실 미분

**리소그래피 손실:**
```
E = ||Litho(M) - Z||² + α·PVBand(M) + β·L_complexity(M)
```
- Z: 타겟 레이아웃
- PVBand: 공정 변동 밴드 (초점/노광량 변동에서 웨이퍼 이미지 변화)
- L_complexity: 마스크 복잡도 페널티

**2단계 통합 학습:**
```
전체 네트워크: UNet → ILT Layer (미분 가능)
L_total = L_print + λ_PW·L_PVBand + λ_c·L_complexity
```

**성능 비교:**
| 방법 | EPE | PVBand | 속도 |
|------|-----|--------|------|
| 순수 ILT | 최선 | 최선 | 느림 |
| ILDLS (제안) | ILT와 유사 | ILT와 유사 | 100~1000× 빠름 |
| 순수 DL | 열등 | 열등 | 가장 빠름 |

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 GNN-OPC 및 ILT 파이프라인 설계에 중요한 참조. ILDLS의 레벨셋 ILT 보정 레이어를 SKOPC의 세그먼트 기반 OPC 보정 후 fine-tuning 단계로 통합 가능. 특히 공정 윈도우 최적화(PWO)와 연계하여 PVBand를 직접 학습 목표로 사용하는 방식은 `skopc/pwo/` 모듈에 통합 가능. 레벨셋 표현은 연속적인 마스크 경계 최적화를 가능하게 하며, 세그먼트 변위 예측의 대안적 표현 방식으로 고려할 수 있다.

## 참고문헌 (핵심)
- Sethian, J.A., "Level set methods and fast marching methods," Cambridge Univ. Press (1999)
- Chan, T. and Vese, L., "Active contours without edges," IEEE Trans. Image Process. (2001)
- Yang, H. et al., "GAN-OPC," DAC 2018
- Liu, X. et al., "Neural-ILT 2.0," TCAD 2022
- Yu, P. and Pan, D.Z., "True process variation aware OPC," JM3 (2007)

## 태그
`Model`, `OPC`, `ILT`, `LevelSet`, `PhysicsInformed`, `DeepLearning`, `UNet`, `MaskOptimization`, `PVBand`, `ProcessWindow`, `HybridModel`, `AppliedOptics`
