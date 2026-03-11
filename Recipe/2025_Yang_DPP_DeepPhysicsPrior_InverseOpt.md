# Deep Generative Prior for First Order Inverse Optimization (DPP)

## 메타데이터
- **저자**: Haoyu Yang, Kamyar Azizzadenesheli, Haoxing Ren
- **연도**: 2025
- **게재지/학회**: arXiv preprint (cs.AI), arXiv:2504.20278 (2025년 4월 제출)
- **DOI/URL**: https://arxiv.org/abs/2504.20278
- **기관**: NVIDIA, Caltech

## 핵심 요약
DPP(Deep Physics Prior)는 역설계 최적화(inverse design optimization)를 위한 1차 그래디언트 기반 방법으로, 사전학습된 보조 신경 연산자(Neural Operator)를 활용하여 사전 분포 제약을 강제한다. 반도체 제조(역리소그래피), 구조 공학, 재료 과학, 유체 역학 등 다양한 역문제에 적용 가능하며, 계산 비용이 높은 생성 AI와 확장성 문제가 있는 베이지안 최적화의 한계를 극복한다. 역리소그래피 응용에서 under-determined/ill-posed 및 저충실도 데이터 조건에서도 강건한 성능을 보인다.

## 주요 기여
- **물리 사전(DPP) 도입**: 신경 연산자 기반 물리 사전으로 역최적화 솔루션 공간 제약
- **1차 방법 가속**: 그래디언트 기반 역최적화의 확장성과 강건성 동시 달성
- **다중 도메인 적용**: 역리소그래피 포함 4개 역설계 도메인에서 검증
- **생성 AI / 베이지안 대안**: 고비용 생성 AI와 확장성 제한 베이지안 최적화의 실용적 대안

## Recipe/Process Flow 상세

### DPP 역리소그래피 최적화 파이프라인

```
관측 결과: 목표 웨이퍼 패턴 T
        ↓
역최적화 문제 정식화:
  M* = argmin_{M} L(F(M), T)
  F: 리소그래피 순방향 모델 (TorchLitho 등)
        ↓
[DPP 사전 제약]
  사전학습된 신경 연산자 G_φ:
  - 역문제의 해 M이 속해야 할 분포를 근사
  - P(M | T) ∝ exp(-L(F(M), T)) · P(M)

  DPP 정규화항:
  L_DPP = L_litho(F(M), T) + λ · ||M - G_φ(T)||²
        ↓
[1차 그래디언트 최적화]
  M_{t+1} = M_t - α · ∇_M L_DPP

  DPP 사전이 최적화를 물리적으로 의미 있는
  솔루션 공간으로 안내
        ↓
최적화된 마스크 M* 출력
```

### DPP의 신경 연산자 역할

**Neural Operator G_φ의 학습**:
- 입력: 타겟 웨이퍼 패턴 T
- 출력: 초기 마스크 추정값 (사전 분포 제공)
- 학습: 수치 ILT 해에서 학습 (대리 모델)

**사전 분포 강제 메커니즘**:
1. 순방향 모델 F(M)로 현재 마스크 평가
2. G_φ(T)와의 거리로 사전 제약 계산
3. 두 항의 가중합으로 최적화 방향 조정

### 역리소그래피 적용 조건
DPP가 특히 효과적인 역리소그래피 시나리오:
- **Under-determined**: 가능한 마스크 해가 여러 개 (사전으로 물리적 해 선택)
- **Ill-posed**: 미세한 타겟 차이가 크게 다른 마스크를 요구하는 불안정 조건
- **저충실도/분포 이탈**: 훈련 분포 밖의 새 패턴에 강건하게 대응

### 생성 AI / 베이지안 최적화와 비교
| 방법 | 계산 비용 | 확장성 | 강건성 | 새 패턴 대응 |
|------|---------|--------|--------|------------|
| 생성 AI | 높음 | 낮음 | 높음 | 보통 |
| 베이지안 최적화 | 중간 | 낮음 | 사전에 민감 | 약함 |
| DPP | **낮음** | **높음** | **높음** | **강함** |

### 다중 도메인 실험
1. **Darcy Flow**: 표준 역문제 (유체 역학)
2. **2D Navier-Stokes**: Under-determined 역문제
3. **역리소그래피**: 저충실도/분포 이탈 조건
4. **구조 최적화**: 재료 역설계

## OPC 툴 구현 관련성
DPP의 물리 사전 접근법은 SKOPC 역문제 해결 향상에 활용 가능:
- **ILT 초기화**: DPP로 수치 ILT의 초기 마스크를 물리적으로 의미 있게 초기화
- **신규 패턴 대응**: 훈련 분포 밖의 새 레이아웃 패턴에 강건한 GNN-OPC 구현
- **TorchLitho 연동**: DPP의 순방향 모델로 TorchLitho 활용하여 물리 제약 반영
- **Under-determined OPC**: 여러 유효 마스크 중 제조 가능성 높은 해를 물리 사전으로 선택

## 참고문헌 (핵심)
- Yang & Ren, "ILILT" (ICML 2024)
- Li et al., "Fourier Neural Operator" (ICLR 2021)
- Yang & Ren, "GPU-Accelerated ILT" (ISPD 2025)
- Chen et al., "DiffOPC" (ICCAD 2024)
- TorchLitho (SPIE 2024)

## 태그
`DPP`, `Deep Physics Prior`, `Neural Operator`, `Inverse Optimization`, `ILT`, `OPC`, `NVIDIA`, `Generative Prior`, `Gradient-based`, `2025`, `Multi-domain`, `arXiv`
