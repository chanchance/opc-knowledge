# Total Source Mask Optimization: High-Capacity, Resist Modeling, and Production-Ready Mask Solution

## 메타데이터
- **저자**: Moutaz Fakhry, Yuri Granik, Kostas Adam, Kafai Lai
- **연도**: 2011
- **게재지/학회**: Proc. SPIE 8166, Photomask Technology 2011, 81663M
- **DOI/URL**: https://doi.org/10.1117/12.898860
- **인용수**: 확인 필요

## 핵심 요약
소스 최적화와 역 리소그래피 마스크 최적화 기법을 반복 프로세스로 결합하여 조명 소스와 마스크 형상을 풀칩 규모에서 동시에 최적화하는 전체 SMO(Total SMO) 흐름을 제안한다. 기존 SMO 기법 대비 패턴 수와 면적을 10배 증가시킨 고용량 처리, 레지스트 모델링, 생산 준비 마스크 솔루션을 통합한다. IBM 및 Mentor Graphics.

## 주요 기여
- 소스 최적화 + ILT 마스크 최적화의 반복 통합 Total SMO 흐름
- 기존 대비 10× 고용량 패턴 처리 능력
- 레지스트 모델링 포함 포괄적 수렴 기준
- 풀칩 규모 생산 준비 마스크 솔루션

## 알고리즘/수식
**Total SMO 반복 흐름:**
```
초기화: m_0 (설계 레이아웃), σ_0 (초기 소스)
반복:
  1. 소스 최적화: σ* = argmin F_SO(σ, m_t)
  2. ILT 마스크 최적화: m_{t+1} = argmin F_ILT(σ*, m)
  3. 수렴 확인: ||m_{t+1} - m_t|| < ε
```

**Total SMO 비용함수 (레지스트 모델 포함):**
$$F_{Total}(\boldsymbol{\sigma}, m) = \sum_{c \in \mathcal{C}_{full}} \sum_j EPE_j^2(\boldsymbol{\sigma}, m; M_{resist}) + \lambda_{PW} F_{PW}$$
레지스트 모델 $M_{resist}$ 포함 풀칩 클립 집합 $\mathcal{C}_{full}$.

**소스 최적화 단계:**
$$\boldsymbol{\sigma}^* = \arg\min_{\boldsymbol{\sigma}} \sum_{c \in \mathcal{C}_{crit}} F_{EPE}(\boldsymbol{\sigma}, m_t)$$

**ILT 마스크 최적화 단계 (레벨셋):**
$$\frac{\partial \phi}{\partial t} = -\delta(\phi) \sum_j \frac{\partial F_{ILT}}{\partial m} \bigg|_{m=\mathcal{H}(\phi)}$$

**고용량 처리 (10× 확장):**
$$|\mathcal{C}_{full}| \approx 10 \times |\mathcal{C}_{conventional}|$$
분산 병렬 처리로 10배 더 많은 클립 최적화.

## OPC 툴 SMO 구현 관련성
- SKOPC Total SMO 반복 최적화 흐름 구현 시 핵심 참고
- `skopc/smo/total_smo.py`에 소스-ILT 마스크 반복 최적화 구현
- 레지스트 모델 포함 SMO는 `skopc/smo/resist_model_smo.py`와 함께 참고
- Pang et al. 2009/2010 풀칩 ILT SMO와 함께 Luminescent/IBM SMO 계열 참고

## 참고문헌 (핵심)
- Pang et al., \"Full chip ILT SMO level set,\" SPIE 2009
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Tian et al., \"Applicability global SMO 22nm,\" SPIE 2011

## 태그
`SMO`, `SPIE`, `total-SMO`, `high-capacity`, `resist-modeling`, `ILT`, `iterative`, `full-chip`, `production-ready`, `IBM`, `Mentor-Graphics`, `level-set`, `source-optimization`
