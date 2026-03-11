# ILILT: Implicit Learning of Inverse Lithography Technologies

## 메타데이터
- **저자**: (ICML 2024 - arxiv:2405.03574)
- **연도**: 2024
- **게재지**: International Conference on Machine Learning (ICML) 2024; arXiv:2405.03574
- **DOI/URL**: https://arxiv.org/abs/2405.03574
- **인용수**: ~15

## 핵심 요약
ILT(Inverse Lithography Technology) 솔버 없이 단일 추론으로 고품질 최적화 마스크를 직접 생성하는 암묵적 학습(implicit layer learning) 프레임워크 ILILT를 제안한다. ILT 최적화 절차를 이해하도록 훈련된 ILILT는 Pix2PixHD 백본과 8단계 언롤링으로 모든 ML 기반 솔루션과 GPU-ILT 수치 솔버보다 EPE 위반을 낮춘다. 기존 ML 초기화 방식(ILT 초기값 생성)을 넘어 ILT 솔버 자체를 대체하는 최초의 end-to-end 암묵적 학습 방법이다.

## 주요 기여
1. ILT 솔버 없이 직접 최적 마스크 생성하는 암묵적 학습 프레임워크
2. Pix2PixHD + 언롤링(8-step unrolling) 구조로 SOTA ML 및 GPU-ILT 능가
3. EPE 위반: ILILT 0.08 vs GPU-ILT 0.21 (2.6배 감소)
4. ILT 수치 솔버의 비볼록 최적화 한계(초기값 의존) 극복

## Recipe/Process Flow 상세

### 기존 ML 기반 ILT 초기화의 한계
```
기존 ML-ILT 접근 (Neural-ILT, DevelSet 등):
  목적: ILT 솔버의 초기값을 ML로 생성 → 수렴 가속
  한계:
    ILT 솔버가 여전히 필요 → 런타임 완전 제거 불가
    ML이 ILT 결과 모방 → ILT 품질에 종속

ILILT 목표:
  ML 모델이 ILT 최적화 절차 자체를 암묵적으로 학습
  → ILT 솔버 없이 직접 고품질 마스크 생성
  → ML 단독으로 ILT 수준 이상의 품질 달성
```

### 암묵적 학습(Implicit Layer Learning) 개념
```
기존 명시적 ML (Explicit):
  L = f_θ(레이아웃)  → 단순 순방향 매핑
  훈련: 지도 학습으로 ILT 결과 모방
  한계: ILT 최적화 구조 무시

암묵적 학습 (Implicit Layer Learning):
  핵심 아이디어: ILT 최적화 스텝을 ML 레이어로 내장
  언롤링(Unrolling): ILT 이터레이션을 미분 가능 레이어로 전개
    L^(t+1) = L^(t) - η × ∇_L Loss(L^(t), target)
  모델 출력: 다수의 언롤링 스텝 후 수렴 마스크
  → ILT 최적화 동역학 내재화

ILILT 구조:
  입력: 타겟 레이아웃 이미지
  내부: Pix2PixHD + 8단계 언롤링 ILT 레이어
  출력: 최적화된 마스크 이미지 (단일 순방향 패스)
```

### Pix2PixHD 백본 + 언롤링
```
Pix2PixHD 백본:
  고해상도 이미지-이미지 변환 (pix2pix 확장)
  다중 스케일 생성기 + 다중 스케일 판별기
  ILT 입출력 고해상도 처리에 적합

언롤링 스텝 (Unrolled Optimization):
  각 스텝: 미분 가능 리소그래피 시뮬 + 마스크 업데이트
  스텝 수 T=8: 효율과 품질 균형 (T=1 대비 +43% EPE 개선)
  역전파: 모든 언롤링 스텝 통과하여 학습

리소그래피 모델 (미분 가능):
  Hopkins 광학 모델 (PyTorch 구현)
  I(M) = sigmoid(Hopkins_response(M))
  → 마스크 M에 대한 미분 가능
```

### 성능 비교
```
EPE 위반 수 (낮을수록 좋음):
  ILILT (Pix2PixHD + 8 unroll): 0.08 [최고]
  GPU-ILT (수치 ILT 솔버):       0.21
  DevelSet (Neural Level Set):   0.35
  Neural-ILT:                    0.52
  GAN-OPC:                       0.78

런타임:
  ILILT 추론: ms 수준 (단일 순방향 패스)
  GPU-ILT: 수 초~수 분/클립

핵심 발견:
  T=1 (단순 ML): GPU-ILT 대비 낮은 품질
  T=8 (ILILT): GPU-ILT보다 우수 → 솔버 대체 가능
  언롤링이 품질의 핵심
```

### 적용 흐름
```
훈련:
  데이터: 타겟 레이아웃 + GPU-ILT 마스크 쌍
  손실: L_EPE + L_ILT_consistency + L_reg
  언롤링 통한 역전파

추론:
  새 타겟 레이아웃 → ILILT → 마스크 (ms 단위)
  ILT 솔버 호출 불필요

장점:
  ILT 솔버 대체: 수 초 → ms 단축
  품질: GPU-ILT 능가 (EPE 위반 2.6× 감소)
  일반화: 언롤링이 ILT 동역학 내재화
```

## OPC 툴 구현 관련성
- **SKOPC ILILT 통합**: `skopc/modeling/openilt_adapter.py`에 ILILT 백엔드 추가 (ILT 솔버 대체)
- **Pix2PixHD 구현**: PyTorch Pix2PixHD 기반 ILILT 모델 구축
- **언롤링 최적화**: TorchLitho 미분 가능 시뮬레이터로 언롤링 스텝 구현
- **품질 기준**: EPE 위반 0.08 달성 목표로 SKOPC ILT 품질 벤치마크

## 참고문헌
- ICML 2024; arXiv:2405.03574 (2024)
- 관련: Neural-ILT (ICCAD 2020 / TCAD 2022)
- 관련: DevelSet (ICCAD 2021 / TCAD 2023)
- 관련: GPU-ILT (cuLitho, NVIDIA 2023)
- 관련: L2O-ILT: Learning to Optimize ILT (TCAD 2024)

## 태그
`Recipe`, `ICML`, `ILT`, `ImplicitLearning`, `MaskOptimization`, `Pix2PixHD`, `Unrolling`, `NeuralNetwork`, `EndToEnd`, `EPE`, `2024`
