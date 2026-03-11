# Open-Source Differentiable Lithography Imaging Framework (TorchLitho)

## 메타데이터
- **저자**: Guojin Chen, Hao Geng, Bei Yu, David Z. Pan
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540J
- **DOI/URL**: https://doi.org/10.1117/12.3009980; GitHub: https://github.com/TorchOPC/TorchLitho
- **인용수**: ~25

## 핵심 요약
리소그래피 연구를 위한 최초의 오픈소스 미분 가능(differentiable) 리소그래피 시뮬레이션 프레임워크 TorchLitho를 제안한다. 미분 가능 프로그래밍과 GPU 연산력을 활용하여 리소그래피 모델링 정밀도를 높이고 RET(Resolution Enhancement Technology) 최적화를 단순화한다. 오픈소스 미분 가능 Abbe 리소그래피 모델, 오픈소스 해석적 레지스트 현상 모델, 벡터 리소그래피 구현을 포함하며, OPC와 SMO 최적화 루프에서 기울기 기반 최적화를 직접 적용 가능하게 한다.

## 주요 기여
1. 최초 오픈소스 미분 가능 Abbe 리소그래피 이미징 모델
2. 최초 오픈소스 해석적 레지스트 현상 모델 (미분 가능)
3. GPU 가속 + PyTorch 기반 → OPC/SMO 기울기 최적화 즉시 적용
4. Neural-ILT, DevelSet, ILILT 등 최신 ML-OPC 연구의 공통 백엔드 인프라

## Recipe/Process Flow 상세

### 미분 가능 리소그래피의 필요성
```
기존 리소그래피 시뮬:
  MATLAB/C++ 기반 독점 코드
  미분 불가능 → 기울기 기반 OPC 최적화 불가
  ML 연구와 통합 어려움

ML-OPC 연구의 공통 과제:
  Neural-ILT, DevelSet, ILILT 각각 자체 시뮬 구현
  코드 재사용 불가 → 중복 개발, 재현성 부족
  공개 표준 벤치마크 없음

TorchLitho 목표:
  오픈소스 미분 가능 시뮬 → 재현 가능한 연구 환경
  PyTorch 통합 → ML 연구와 즉시 결합
  GPU 가속 → 실용적 속도
```

### 핵심 구성요소

#### Abbe 모델 (비가간섭성 이미징)
```
Abbe 이미징 모델:
  I(x) = Σ_s |∫ P(f) × Ô(f - f_s) × exp(2πi f·x) df|²
  P(f): 투영 렌즈 동공 함수
  Ô(f): 마스크 스펙트럼
  f_s: 소스점 주파수

PyTorch 구현:
  FFT: torch.fft.fft2/ifft2 (GPU 가속)
  동공 함수: 해석적 표현 (NA, σ 파라미터)
  소스: 픽셀화된 조명 분포
  미분 가능: autograd로 ∂I/∂M 자동 계산

Hopkins 모델 (TCC 기반):
  I(x) = Σ_k λ_k |h_k * M|²
  TCC 분해: SOCS (Sum of Coherent Sources)
  속도: Abbe 대비 빠름 (SOCS 수에 따라)
```

#### 레지스트 현상 모델
```
해석적 레지스트 모델:
  임계값 기반: resist_image = sigmoid((I - I_th) / σ_blur)
  Gaussian 블러: 레지스트 확산 효과 모델링
  미분 가능: 항공 이미지 → 레지스트 이미지 → EPE

레지스트 파라미터:
  I_th: 노광 임계값
  σ_blur: 레지스트 블러 (nm)
  → 실제 공정 캘리브레이션으로 결정
```

#### OPC/SMO 최적화 통합
```
OPC 최적화:
  목적함수: L_EPE = ||resist_image(M) - target||²
  기울기: ∂L/∂M = autograd로 자동 계산
  업데이트: M ← M - lr × ∂L/∂M
  → 기울기 기반 ILT 즉시 구현

SMO 최적화:
  목적함수: L_SMO(S, M) = L_EPE + λ × L_PVB
  S: 소스 조명 분포 (픽셀화)
  M: 마스크 패턴
  동시 최적화: ∂L/∂S, ∂L/∂M 동시 계산

ML-OPC 통합:
  신경망 출력 → TorchLitho 시뮬 → 손실 계산
  역전파: 손실 → TorchLitho → 신경망 가중치
  → Neural-ILT, DevelSet, ILILT 등의 표준 백엔드
```

### 성능
```
속도 (GPU vs CPU):
  GPU (CUDA): CPU 대비 수십~수백 배 빠름
  배치 처리: 다수 클립 병렬 시뮬

정확도:
  PROLITH 등 상용 툴과 비교 → 동등 수준
  OPC 결과: 기존 그래디언트 ILT와 비교 가능

오픈소스 접근성:
  GitHub: https://github.com/TorchOPC/TorchLitho
  MIT 라이선스: 연구/상업 모두 자유 사용
  pip 설치 가능: pip install torchlitho
```

## OPC 툴 구현 관련성
- **SKOPC 핵심 백엔드**: `skopc/modeling/litho_engine.py`에 TorchLitho 기반 시뮬레이터 통합
- **미분 가능 OPC**: TorchLitho로 SKOPC ILT 최적화 루프 구현 (기울기 기반)
- **SMO 백엔드**: TorchLitho Abbe 모델 + SMO 최적화 결합
- **ML 훈련 인프라**: Neural-ILT, GAN-OPC 등 ML-OPC 모델 훈련을 위한 리소그래피 손실 계산

## 참고문헌
- Proc. SPIE 12954, DTCO and Computational Patterning III (April 2024)
- GitHub: https://github.com/TorchOPC/TorchLitho
- 저자 소속: CUHK (Bei Yu 그룹) + UT Austin (David Z. Pan 그룹)
- 관련: TorchResist open-source differentiable resist simulator (SPIE 2025)
- 관련: Neural-ILT (ICCAD 2020), DevelSet (ICCAD 2021), ILILT (ICML 2024)

## 태그
`Recipe`, `SPIE`, `TorchLitho`, `OpenSource`, `Differentiable`, `LithographySimulation`, `Abbe`, `Hopkins`, `OPC`, `SMO`, `GPU`, `PyTorch`, `CUHK`, `BeiYu`, `2024`
