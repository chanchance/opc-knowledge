# Open-Source Differentiable Lithography Imaging Framework (TorchLitho)

## 메타데이터
- **저자**: Guojin Chen, Hao Geng, Bei Yu, David Z. Pan
- **연도**: 2024
- **게재지/학회**: SPIE Advanced Lithography 2024, arXiv:2409.15306
- **DOI/URL**: https://arxiv.org/abs/2409.15306 / https://github.com/TorchOPC/TorchLitho
- **인용수**: N/A (2024 신규)

## 핵심 요약
TorchLitho는 반도체 리소그래피의 핵심 구성 요소를 미분 가능(differentiable)한 세그먼트로 모델링하여 GPU 가속 그래디언트 기반 최적화를 가능하게 하는 오픈소스 프레임워크다. Abbe 모델과 Hopkins 모델을 포함한 표준 스칼라 이미징 모델과 근사 모델을 구현하며, 해상도 향상 기술(RET) 최적화에 직접 활용 가능하다. SKOPC의 `TorchLitho` 의존성과 직접 연결되는 핵심 참조 구현체다.

## 주요 기여
- **미분 가능 리소그래피 파이프라인**: 전체 이미징 파이프라인을 그래디언트 최적화 가능한 형태로 구조화
- **오픈소스 공개**: 반도체 리소그래피 연구의 재현성과 협업 촉진
- **다중 이미징 모델**: Abbe, Hopkins, 근사 모델 통합 구현
- **GPU 가속**: PyTorch 기반 GPU 연산으로 리소그래피 시뮬레이션 가속

## Recipe/Process Flow 상세

### TorchLitho 프레임워크 아키텍처

```
[리소그래피 이미징 파이프라인 (미분 가능)]

1. 조명 모델 (Illumination Model)
   - 부분 간섭성(Partial Coherence) 설정
   - 조명 형상: 디스크, 환형(Annular), 쿼드러폴, 디포커스 등
   - σ (부분 간섭도) 파라미터

2. 마스크 모델 (Mask Model)
   - 이진 마스크 또는 위상 시프팅 마스크(PSM)
   - 마스크 3D 효과 근사 (EUV용)

3. 투영 광학계 (Projection Optics)
   - NA (Numerical Aperture)
   - 애버레이션 (Zernike 다항식)
   - 이미징 파장 λ

4. 공중 이미지 계산 (Aerial Image)
   [Abbe 모델]:
   I(x,y) = ΣΣ J(f,g)|P(f,g)|²|M̃(f,g)|² → 비간섭성 합산

   [Hopkins 모델]:
   I(x,y) = ΣΣΣ TCC(f₁,g₁;f₂,g₂)·M̃(f₁,g₁)·M̃*(f₂,g₂)
   TCC: 전송 크로스 계수 (Transmission Cross Coefficient)

5. 레지스트 모델 (Resist Model)
   - 임계값 모델 (Threshold Model)
   - 확산 모델 (Diffusion Model)
   - 레지스트 윤곽 계산

6. 손실 계산 & 역전파
   L = ||I_resist - T||² → ∂L/∂M (마스크에 대한 그래디언트)
```

### 구현된 모델
| 모델 | 설명 | 연산 복잡도 | 정확도 |
|------|------|------------|--------|
| Abbe | 비간섭성 합산 기반 | O(N⁴) | 높음 |
| Hopkins | TCC 기반 (SOCS 근사 포함) | O(N² × k) | 높음 |
| SOCS | Hopkins 근사 (k개 고유모드) | O(k × N²) | 중간-높음 |
| Threshold | 단순 임계값 레지스트 | O(N²) | 낮음 |

### RET 최적화 활용
TorchLitho는 다음 RET 최적화에 직접 활용:
- **OPC**: 마스크 패턴 최적화 (마스크에 대한 그래디언트)
- **SMO**: 조명 형상 최적화 (조명 파라미터에 대한 그래디언트)
- **SRAF**: 보조 피처 배치 최적화
- **PSM**: 위상 시프팅 마스크 최적화

### PyTorch API 구조 (GitHub 기반)
```python
# TorchLitho 핵심 모듈
from torchlitho import LithoSim, AerialImage, ResistModel

# 시뮬레이터 초기화
litho = LithoSim(
    wavelength=193,    # nm (ArF 또는 EUV)
    NA=1.35,           # 침지 리소그래피
    sigma=0.8,         # 부분 간섭도
    model='Hopkins'    # 이미징 모델 선택
)

# 미분 가능 순전파
aerial = litho.forward(mask)  # mask: torch.Tensor (미분 가능)
resist_contour = resist_model(aerial)

# 손실 및 역전파
loss = criterion(resist_contour, target)
loss.backward()  # mask.grad 자동 계산
```

## OPC 툴 구현 관련성
TorchLitho는 SKOPC의 직접적 의존성으로 핵심적 관련성 보유:
- **직접 연동**: `skopc/modeling/litho_engine.py`가 TorchLitho를 직접 의존
- **Hopkins 모델**: SKOPC의 기본 리소그래피 시뮬레이션 엔진
- **미분 가능 OPC**: GNN-OPC 학습 시 리소그래피 손실의 역전파에 필수
- **SMO 통합**: SKOPC SMO 모듈의 조명 최적화에 TorchLitho 그래디언트 활용
- **EUV 지원**: 마스크 3D 효과 모델을 추가하여 EUV OPC 레시피 개발 가능

## 참고문헌 (핵심)
- Hopkins, "On the diffraction theory of optical images" (Proc. Royal Society, 1953)
- Abbe, "Beiträge zur Theorie des Mikroskops" (1873)
- Cobb et al., "Fast sparse aerial image calculation for OPC" (SPIE 1995)
- Chen et al., "DiffOPC" (ICCAD 2024)
- TorchOPC/TorchLitho GitHub repository (2024)

## 태그
`TorchLitho`, `Open Source`, `Differentiable Lithography`, `Hopkins Model`, `Abbe Model`, `SOCS`, `PyTorch`, `GPU`, `RET`, `OPC`, `SMO`, `SPIE 2024`, `2024`
