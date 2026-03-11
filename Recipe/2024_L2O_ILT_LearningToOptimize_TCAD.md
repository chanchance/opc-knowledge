# L2O-ILT: Learning to Optimize Inverse Lithography Techniques

## 메타데이터
- **저자**: Binwu Zhu, Su Zheng, Ziyang Yu, Guojin Chen, Yuzhe Ma, Fan Yang, Bei Yu, Martin Wong
- **연도**: 2024
- **게재지**: IEEE Transactions on Computer-Aided Design (TCAD), Vol. 43, No. 9, pp. 2755–2768 (2024)
- **DOI/URL**: https://doi.org/10.1109/TCAD.2023.3323164
- **인용수**: ~20

## 핵심 요약
ILT(Inverse Lithography Technology)의 반복 최적화 알고리즘을 학습 가능한 신경망으로 언롤링(unrolling)하는 L2O-ILT 프레임워크를 제안한다. ILT 초기값 생성에 고품질 신경망 초기화를 제공하며, 교대 최적화(alternating optimization) 메커니즘과 적응적 해 공간(adaptive solution space) 방법을 결합하여 공정 변동 밴드(PV Band)와 마스크 인쇄 가능성을 동시에 개선한다. CUHK Bei Yu 그룹의 ILT 연구 시리즈(Neural-ILT, DevelSet, ILILT) 후속 작업으로 TCAD 2024에 게재되었다.

## 주요 기여
1. ILT 반복 최적화를 학습 가능 신경망으로 언롤링 (해석 가능성 높음)
2. 교대 최적화: 타겟 구동 + PV Band 구동 최적화 교대 수행
3. 적응적 해 공간 방법으로 기존 ILT 알고리즘 개선
4. 마스크 인쇄 가능성 + 런타임 모두 이전 방법 대비 향상

## Recipe/Process Flow 상세

### L2O-ILT의 설계 동기
```
기존 ILT 문제:
  느린 수렴: 수백~수천 이터레이션 필요
  국소 최적: 비볼록 문제 → 초기값 의존성
  PV Band 최적화 부재: 명목 조건만 최적화하는 경우 많음

ML 기반 ILT 초기화 방법 (Neural-ILT, DevelSet):
  단일 순방향 패스 → ILT 초기값 생성
  장점: 빠른 ILT 수렴
  한계: 초기값만 생성 → ILT 솔버 여전히 필요

L2O-ILT 목표:
  ILT 최적화 알고리즘 자체를 학습 (optimizer learning)
  → 더 좋은 초기값 + 더 스마트한 ILT 갱신 규칙
```

### L2O (Learning to Optimize) 프레임워크
```
핵심 개념: ILT 이터레이션을 미분 가능 레이어로 언롤링

표준 ILT 업데이트 (기울기 기반):
  M^(t+1) = M^(t) - η × ∇_M L_litho(M^(t))
  문제: 스텝 크기 η 고정, 하이퍼파라미터 민감

L2O 언롤링:
  각 ILT 스텝을 신경망 레이어로 대체:
    M^(t+1) = M^(t) - LSTM_θ(∇_M L_litho(M^(t)), M^(t))
  LSTM: 기울기 + 현재 마스크 → 최적 업데이트 방향 학습
  훈련: 전체 ILT 궤적에서 역전파
  결과: 더 빠른 수렴, 더 좋은 최종 마스크

해석 가능성:
  언롤링 구조 → ILT 이터레이션 직접 대응 → 물리적 의미 보존
```

### 교대 최적화 (Alternating Optimization)
```
두 가지 최적화 목표:
  목표 1: L_nominal (명목 조건 인쇄 가능성)
    타겟 드리븐 최적화:
      M ← arg min EPE_nominal(M)

  목표 2: L_PVB (공정 변동 밴드)
    PV Band 드리븐 최적화:
      M ← arg min PVBand(M, {F, D 변동})

교대 수행:
  이터레이션 t=1,3,5,...: 타겟 드리븐 최적화
  이터레이션 t=2,4,6,...: PV Band 드리븐 최적화
  효과:
    PV Band 크게 감소 (공정 마진 향상)
    L_nominal (명목 EPE)는 약간 영향 (허용 범위 내)
```

### 적응적 해 공간 방법
```
문제: ILT 마스크 탐색 공간이 너무 넓음
  → 일부 마스크 영역은 이미 수렴
  → 전체 재최적화 비효율

적응적 해 공간:
  수렴된 마스크 픽셀: 업데이트 억제 (마스크 고정)
  미수렴 픽셀: 집중 최적화
  구현: 픽셀별 학습률 마스크 (adaptive masking)
  효과: 수렴 속도 ↑, 최적해 품질 ↑
```

### 성능 결과
```
기준: 이전 SOTA ML ILT 방법들 (Neural-ILT, DevelSet)

마스크 인쇄 가능성 (EPE 위반):
  L2O-ILT: 이전 SOTA 대비 15~20% EPE 위반 감소

PV Band:
  교대 최적화 적용: 단순 ILT 대비 PV Band 크게 감소
  공정 마진 향상

런타임:
  L2O-ILT: 고품질 초기화 → ILT 수렴 이터레이션 감소
  전체 TAT: 이전 방법 대비 단축
```

## OPC 툴 구현 관련성
- **SKOPC L2O-ILT**: `skopc/modeling/openilt_adapter.py`에 L2O-ILT 초기화 백엔드 추가
- **LSTM 기반 업데이트**: ILT 이터레이션 시 LSTM 기반 업데이트 규칙 학습
- **교대 최적화**: PV Band 드리븐 최적화와 타겟 드리븐 최적화 교대 적용
- **공정 마진**: L2O-ILT의 PV Band 최적화로 SKOPC PWO 연계

## 참고문헌
- IEEE TCAD, Vol. 43, No. 9, pp. 2755–2768 (2024)
- 저자 소속: CUHK (Bei Yu group) + 교내 협력
- 관련: Neural-ILT (ICCAD 2020 / TCAD 2022)
- 관련: DevelSet (ICCAD 2021 / TCAD 2023)
- 관련: ILILT (ICML 2024)
- 관련: A2-ILT (DAC 2022)

## 태그
`Recipe`, `IEEE`, `TCAD`, `ILT`, `LearningToOptimize`, `L2O`, `UnrolledOptimization`, `AlternatingOptimization`, `PVBand`, `MaskPrintability`, `CUHK`, `BeiYu`, `2024`
