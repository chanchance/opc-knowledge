# Neural-ILT: Migrating ILT to Neural Networks for Mask Printability and Complexity Co-optimization

## 메타데이터
- **저자**: Bentian Jiang, Lixin Liu, Yuzhe Ma, Hang Zhang, Bei Yu, Evangeline F.Y. Young
- **연도**: 2020
- **게재지**: IEEE/ACM International Conference on Computer-Aided Design (ICCAD) 2020; 확장판: IEEE TCAD 2022
- **DOI/URL**: https://ieeexplore.ieee.org/document/9256592
- **인용수**: ~80

## 핵심 요약
ILT(Inverse Lithography Technology)를 신경망으로 완전히 대체하는 엔드 투 엔드 학습 기반 마스크 최적화 프레임워크 Neural-ILT를 제안한다. 단일 신경망이 마스크 인쇄 가능성 향상, 마스크 복잡도 최적화, 흐름 가속화의 세 목표를 동시에 달성한다. 기존 최고의 학습 기반 OPC 대비 30~70배 TAT 단축, 낮은 마스크 복잡도, 동등한 인쇄 가능성을 달성한다.

## 주요 기여
1. ILT를 완전히 신경망으로 구현하는 엔드 투 엔드 마스크 최적화기
2. 인쇄 가능성 + 마스크 복잡도 동시 최적화 (3가지 목표 통합)
3. 기존 SOTA 학습 기반 OPC 대비 30~70× TAT 단축
4. CUHK EDA 그룹 오픈소스: github.com/cuhk-eda/neural-ilt

## Recipe/Process Flow 상세

### Neural-ILT의 설계 목표
```
기존 ILT의 문제:
  1. 느림: 클립당 수 초~수 분 (반복 최적화)
  2. 마스크 복잡도: 제약 없으면 제조 불가 형상
  3. 단목적: 인쇄 가능성만 최적화

Neural-ILT의 세 목표:
  (1) 마스크 인쇄 가능성: EPE 최소화, 공정 윈도우 확보
  (2) 마스크 복잡도: 단순한 형상, MRC 준수
  (3) 흐름 가속: 실용적 TAT 달성

트레이드오프 균형:
  인쇄 가능성 ↑ → 복잡도 ↑ (ILT의 본질적 긴장)
  Neural-ILT: 정규화 항으로 균형 달성
```

### 신경망 아키텍처
```
U-Net 기반 인코더-디코더:
  입력: 타겟 레이아웃 이미지 (L × W 픽셀)
  출력: 최적 마스크 이미지 (같은 해상도)

인코더 (다운샘플링):
  Convolution → BatchNorm → ReLU × 여러 층
  맥락 정보 압축: 광학 근접 효과 범위 포착

디코더 (업샘플링):
  Transposed Conv → BN → ReLU × 여러 층
  Skip connections: 세부 패턴 정보 보존
  최종층: Sigmoid (이진 마스크 확률 출력)

마스크 이진화:
  연속 출력 → 이진 마스크 (0 또는 1)
  Straight-Through Estimator (STE): 역전파 유지
```

### 손실 함수 (3목적 통합)
```
L_total = L_print + λ_c × L_complex + λ_r × L_reg

인쇄 가능성 손실 L_print:
  L_print = ||I(M) - I_target||²
  I(M): 마스크 M의 리소그래피 시뮬 이미지
  → 미분 가능 리소그래피 시뮬레이터 필요

마스크 복잡도 손실 L_complex:
  L_complex = ||M||_0 (비영 픽셀 수)
  근사: L_complex = ||M||_1 (L1 정규화, 미분 가능)
  또는: Total Variation (경계 길이 최소화)
  → SRAF 수 감소, 형상 단순화

정규화 L_reg:
  L_reg = BinaryCrossEntropy(M, M_binary)
  이진 마스크를 향한 부드러운 압력
  → 그레이 픽셀 억제
```

### 훈련 및 추론
```
훈련:
  데이터: 공개 GAN-OPC 데이터셋 (~4000 클립)
  Ground truth: 표준 ILT로 생성
  손실: 역전파 + Adam 최적화
  미분 가능 시뮬레이터: PyTorch Hopkins 광학 모델

추론:
  타겟 레이아웃 → Neural-ILT → 마스크 (단일 순방향 패스)
  추론 시간: ~ms (GPU) → "즉시" 마스크

선택적 후처리:
  마스크 이진화 검증
  MRC 검사 + 보정
  표준 OPC 소수 이터레이션 (선택)
```

### 성능 결과
```
SOTA 학습 기반 OPC (GAN-OPC) 대비:
  TAT: 30~70× 단축 (단일 순방향 패스 덕분)
  마스크 복잡도: 감소 (L_complex 덕분)
  마스크 인쇄 가능성: 동등

표준 ILT 대비:
  TAT: 수십~수백 배 빠름
  마스크 복잡도: 낮음 또는 동등
  인쇄 가능성: 약간 낮지만 허용 범위

Neural-ILT 2.0 (TCAD 2022):
  도메인 특화 가속, 더 강건한 훈련
  추가 성능 향상
```

## OPC 툴 구현 관련성
- **SKOPC Neural-ILT 통합**: `skopc/modeling/openilt_adapter.py`에 Neural-ILT 백엔드 추가 옵션
- **미분 가능 시뮬레이터**: TorchLitho를 Neural-ILT의 L_print 계산에 활용
- **마스크 복잡도 제어**: 복잡도 손실 λ_c로 SRAF 수와 형상 복잡도 조절
- **오픈소스 활용**: github.com/cuhk-eda/neural-ilt 코드 참조로 SKOPC Neural-ILT 구현

## 참고문헌
- IEEE/ACM ICCAD 2020; IEEE TCAD 2022
- 저자 소속: CUHK (Bei Yu group)
- GitHub: github.com/cuhk-eda/neural-ilt
- 관련: GAN-OPC (DAC 2018 / TCAD 2020)
- 관련: DevelSet (ICCAD 2021 / TCAD 2023)
- 관련: OpenILT (ISEDA 2024)

## 태그
`Recipe`, `IEEE`, `ICCAD`, `TCAD`, `ILT`, `NeuralNetwork`, `EndToEnd`, `MaskOptimization`, `MaskComplexity`, `Printability`, `CUHK`, `BeiYu`, `OpenSource`, `2020`
