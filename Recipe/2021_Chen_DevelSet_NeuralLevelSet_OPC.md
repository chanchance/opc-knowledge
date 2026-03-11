# DevelSet: Deep Neural Level Set for Instant Mask Optimization

## 메타데이터
- **저자**: Guojin Chen, Hongquan He, Peng Xu, Haoyu Yang, Bei Yu
- **연도**: 2021 (ICCAD), 2023 (IEEE TCAD 확장)
- **게재지**: IEEE/ACM ICCAD 2021; IEEE Transactions on Computer-Aided Design (TCAD), Vol. 42, No. 12 (2023)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10153412
- **인용수**: ~60

## 핵심 요약
레벨 셋(Level Set) 기반 ILT를 신경망으로 가속화하는 DevelSet 프레임워크를 제안한다. GPU 가속 레벨 셋 최적화기(DevelSet-Optimizer)와 신경망 초기화기(DevelSet-Net)로 구성되며, 곡률 항(curvature term)으로 마스크 복잡도를 제어한다. DevelSet-Net이 신경망 추론으로 수렴에 가까운 초기 레벨 셋 함수를 생성하고, Optimizer가 소수 이터레이션으로 최종 수렴한다. 기존 ILT 대비 수백 배 빠른 "즉시(instant)" 마스크 최적화를 달성한다.

## 주요 기여
1. 레벨 셋 OPC/ILT에 곡률 항 도입으로 마스크 복잡도 제어
2. GPU 가속 레벨 셋 최적화기로 계산 병목 해소
3. 신경망(DevelSet-Net)으로 최적에 가까운 레벨 셋 초기화 제공
4. CUHK OpenILT 플랫폼에 통합된 오픈소스 구현

## Recipe/Process Flow 상세

### 레벨 셋 ILT와 DevelSet의 관계
```
표준 레벨 셋 ILT:
  마스크 표현: M(x,y) = H(φ(x,y))
    φ: 레벨 셋 함수, H: Heaviside 함수
  최적화:
    min_φ ||I(H(φ)) - I_target||² + λ_M R(M)
    → 그래디언트 하강으로 φ 업데이트

  문제:
    1. 마스크 복잡도 제어 어려움
       → 복잡한 형상 → 마스크 제작 어려움
    2. 수렴 속도 느림 (수백 이터레이션)
    3. GPU 병렬화 비효율적

DevelSet 개선:
  1. 곡률 항 추가 → 마스크 복잡도 제어
  2. GPU 최적화 알고리즘 → 속도 향상
  3. 신경망 초기화 → 이터레이션 수 감소
```

### DevelSet-Optimizer (GPU 가속 레벨 셋)
```
곡률 항 도입:
  L_total = L_litho + λ_M ||M|| + λ_κ ||κ(φ)||
  κ(φ): 레벨 셋 함수의 곡률
  λ_κ: 곡률 정규화 강도

  효과:
    λ_κ 크면 → 부드러운(곡률 작은) 마스크 → 제조 용이
    λ_κ 작으면 → 복잡한 형상 허용 → 더 좋은 OPC 성능
    균형 조정으로 제조 가능성 + OPC 품질 동시 달성

GPU 친화적 알고리즘:
  1. 레벨 셋 함수를 픽셀 격자로 표현 (GPU 텐서)
  2. 그래디언트 계산: CUDA 커널로 병렬화
  3. 배치 처리: 여러 클립 동시 최적화
  4. 리소그래피 시뮬: PyTorch FFT (GPU)

성능:
  표준 CPU ILT 대비: ~100× 속도 향상
  GPU 배치 처리로 추가 확장 가능
```

### DevelSet-Net (신경망 초기화)
```
설계 목표:
  새 타겟 입력 시 수렴에 가까운 φ_init 즉시 생성
  → Optimizer의 이터레이션 수 감소

신경망 아키텍처:
  입력: 타겟 패턴 이미지 (256×256 또는 512×512)
  출력: 초기 레벨 셋 함수 φ_init
  구조: U-Net 또는 인코더-디코더 (skip connections)
  변조(Modulation) 브랜치:
    곡률 비용 보상을 위한 추가 브랜치
    φ_init = f_base(target) + f_modulation(target, λ_κ)

훈련:
  손실: ||φ_init - φ_optimal||² + L_litho(H(φ_init))
  데이터: (타겟, Optimizer로 수렴된 최적 φ) 쌍
  정규화: Dropout, L2

추론 단계:
  target → DevelSet-Net → φ_init
  φ_init → DevelSet-Optimizer (소수 이터레이션)
  → 최종 마스크
```

### DevelSet 전체 흐름
```
오프라인 (훈련):
  1. Optimizer로 충분한 설계에서 최적 φ 생성
  2. DevelSet-Net 훈련

온라인 (추론):
  1. target → DevelSet-Net → φ_init (ms)
  2. φ_init → DevelSet-Optimizer (~10 이터레이션)
  3. H(φ) → 최종 마스크

성능:
  전통 ILT (수백 iter): 수 분~수십 분/클립
  DevelSet (net + ~10 iter): 수 초/클립
  순수 net 추론: ms
  → "Instant" 마스크 최적화 달성
```

### OpenILT 통합
```
오픈소스 플랫폼:
  GitHub: github.com/OpenOPC/OpenILT
  CUHK Bei Yu 그룹 유지 관리

포함 구성요소:
  - 기본 ILT 구현
  - GAN-OPC
  - DevelSet
  - Neural-ILT
  - 공통 데이터셋 및 평가 코드
```

### 성능 결과 (ICCAD 2021, TCAD 2023)
```
마스크 품질 (L2, PVB):
  DevelSet > 표준 레벨 셋 ILT (곡률 제어 덕분)
  Manhattan OPC 대비 공정 윈도우 향상

런타임:
  표준 CPU ILT: 기준 (100%)
  DevelSet-Optimizer: ~1% (GPU 가속)
  DevelSet (Net + Opt): ~0.1% → "Instant"

마스크 복잡도:
  곡률 항으로 기존 ILT 대비 감소
  제조 가능성 향상 (MBMW 제작 적합)
```

## OPC 툴 구현 관련성
- **SKOPC openilt_adapter 확장**: `skopc/modeling/openilt_adapter.py`에 DevelSet 백엔드 추가
- **레벨 셋 표현**: 기존 픽셀/엣지 표현을 레벨 셋으로 전환하는 마스크 변환 모듈
- **PyTorch 기반 GPU**: TorchLitho와 DevelSet 통합으로 end-to-end GPU 가속 ILT
- **곡률 제어**: SKOPC 레시피에 mask_complexity_weight 파라미터로 DevelSet 곡률 강도 설정

## 참고문헌
- IEEE/ACM ICCAD 2021; IEEE TCAD 42(12) (2023)
- 저자 소속: CUHK (Bei Yu group)
- 관련: GAN-OPC (DAC 2018 / TCAD 2020)
- 관련: Neural-ILT (ICCAD 2020)
- 관련: OpenILT 플랫폼 (ISEDA 2024)

## 태그
`Recipe`, `IEEE`, `TCAD`, `ICCAD`, `ILT`, `LevelSet`, `NeuralNetwork`, `GPU`, `MaskOptimization`, `Curvature`, `OpenILT`, `CUHK`, `BeiYu`, `2021`, `2023`
