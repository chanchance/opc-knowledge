# GPU-Accelerated Inverse Lithography Towards High Quality Curvy Mask Generation

## 메타데이터
- **저자**: (arXiv:2411.07311 - ISPD 2025)
- **연도**: 2024 (게재 2025)
- **게재지**: Proceedings of the 2025 International Symposium on Physical Design (ISPD 2025)
- **DOI/URL**: https://doi.org/10.1145/3698364.3705343; arXiv:2411.07311
- **인용수**: ~5

## 핵심 요약
커비리니어(curvilinear) 마스크 생성을 위한 GPU 가속 ILT 알고리즘을 제안한다. 미분 가능 형태학적 연산(differentiable morphological operations)을 최적화 프레임워크에 통합하여 마스크 설계 규칙 위반을 후처리가 아닌 최적화 중에 능동적으로 처리한다. 커비리니어 설계 리타겟팅(retargeting)과 향상된 최적화 전략을 결합하여 리딩 ILT 엔진 대비 MSE, PV 밴드, EPE 모두에서 유의미한 성능 향상을 달성한다.

## 주요 기여
1. 미분 가능 형태학적 연산(에로전/딜레이션)으로 MRC를 최적화에 통합
2. 커비리니어 설계 리타겟팅으로 빠른 ILT 수렴
3. GPU 가속으로 전체 칩 커비리니어 ILT 실용화
4. MSE, PVB, EPE 모두 SOTA ILT 엔진 대비 유의미한 개선

## Recipe/Process Flow 상세

### 커비리니어 ILT의 동기
```
기존 Manhattan ILT:
  마스크 형상: 직교 모서리 (직각)
  제약: 마스크 패터닝 장비(e-beam)의 전통적 한계
  장점: 마스크 데이터 처리 단순
  단점: 직각 형상 → 리소그래피 최적화 제한

커비리니어 ILT:
  마스크 형상: 자유 형상 (곡선 가능)
  장점:
    더 높은 인쇄 가능성 (EPE ↓)
    더 넓은 공정 윈도우 (PV Band ↓)
  필요 조건:
    MBMW(Multi-Beam Mask Writer) 등 최신 마스크 리소그래피
    MRC(Mask Rule Check): 커비리니어 형상 제조 가능성 검증

핵심 과제:
  커비리니어 MRC 후처리 → 최적화 후 MRC 위반 수정
  문제: 후처리 수정이 ILT 최적화 결과 왜곡
  해결: MRC를 최적화 중 능동적으로 처리
```

### 미분 가능 형태학적 연산
```
마스크 설계 규칙 (MRC) 종류:
  최소 선폭: 마스크 패턴 최소 폭 제약
  최소 이격: 패턴 간 최소 거리 제약
  코너 라운딩: 날카로운 코너 금지

형태학적 연산:
  에로전(Erosion): M_eroded = M ⊖ B
  팽창(Dilation): M_dilated = M ⊕ B
  오프닝(Opening): erosion 후 dilation → 작은 돌출 제거
  클로징(Closing): dilation 후 erosion → 작은 구멍 채움

미분 가능 구현 (PyTorch):
  불연속 이진 연산 → 부드러운 근사:
    Erosion(M, B) ≈ min_{b∈B}(M shifted by b)
    → softmin으로 근사하여 미분 가능하게
  역전파 가능 → 최적화 루프에 직접 통합

MRC 손실:
  L_MRC = ||M - Opening(M, B_min)||²  (최소 선폭 강제)
        + ||M - Closing(M, B_min)||²  (최소 이격 강제)
  최적화: L_total = L_litho + λ_MRC × L_MRC
```

### 커비리니어 설계 리타겟팅
```
리타겟팅 (Retargeting) 개념:
  ILT 초기값을 단순히 타겟 레이아웃 → 리타겟 레이아웃으로 변환
  목적: ILT 수렴 가속 + 더 좋은 초기값 제공

커비리니어 리타겟팅:
  직교 타겟 → 커비리니어 초기 마스크 생성
  방법: 코너 라운딩 + 세그먼트 이동
  효과:
    ILT 초기값이 이미 커비리니어 → 수렴 빠름
    직각에서 멀어짐 → MRC 위반 줄어듦

GPU 가속:
  PyTorch 형태학적 연산 + ILT 기울기: GPU에서 병렬 처리
  배치 처리: 다수 클립 동시 최적화
  CUDA 최적화: FFT 기반 리소그래피 시뮬 가속
```

### 성능 결과
```
비교 대상: 리딩 학술 ILT 엔진 (GAN-OPC, DevelSet, GPU-ILT)

MSE (인쇄 이미지 품질):
  유의미한 감소 → 더 정확한 타겟 인쇄

PV Band (공정 변동 마진):
  감소 → 더 넓은 공정 윈도우

EPE 위반:
  감소 → 더 적은 패턴 오차

MRC 준수:
  최적화 중 능동 처리 → 후처리 수정 최소화
  → 커비리니어 마스크 제조 가능성 향상
```

## OPC 툴 구현 관련성
- **SKOPC 커비리니어 ILT**: `skopc/modeling/openilt_adapter.py`에 커비리니어 MRC 통합
- **미분 가능 형태학적 연산**: TorchLitho + PyTorch로 에로전/딜레이션 구현
- **커비리니어 리타겟팅**: OPC 실행 전 커비리니어 마스크 초기화 사전 처리
- **MBMW 연동**: 커비리니어 마스크 데이터를 MBMW 포맷으로 변환 출력

## 참고문헌
- ISPD 2025; arXiv:2411.07311 (November 2024)
- 관련: cuLitho GPU OPC (NVIDIA, 2023)
- 관련: DevelSet Neural Level Set (ICCAD 2021 / TCAD 2023)
- 관련: Curvilinear mask OPC flow (SPIE 12495, 2023)
- 관련: A2-ILT (DAC 2022)

## 태그
`Recipe`, `ISPD`, `ILT`, `Curvilinear`, `GPU`, `MorphologicalOperations`, `MaskRuleCheck`, `DifferentiableOptimization`, `ProcessWindow`, `MaskGeneration`, `2024`, `2025`
