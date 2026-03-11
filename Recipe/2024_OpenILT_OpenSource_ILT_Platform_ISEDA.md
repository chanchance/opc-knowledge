# OpenILT: An Open-Source Inverse Lithography Technique Framework

## 메타데이터
- **저자**: Su Zheng, Ziyang Yu, Guojin Chen, Yuzhe Ma, Bei Yu, Martin D.F. Wong
- **연도**: 2024
- **게재지**: 2024 IEEE 2nd International Symposium on Electronics Design Automation (ISEDA), Xi'an, China
- **DOI/URL**: https://ieeexplore.ieee.org/document/10396314
- **인용수**: ~15

## 핵심 요약
ILT 연구를 위한 오픈소스 플랫폼 OpenILT를 제안한다. PyTorch 프레임워크 기반으로 GPU 가속과 FFT 연산을 통합하여 전체 칩 데이터의 병렬 처리를 지원하며, 리소그래피 시뮬레이션, 초기화, 최적화, 평가 등 ILT 흐름의 각 구성요소를 분리하여 모듈식 유연한 프레임워크를 제공한다. AI 기반 ILT 방법 구현과 평가를 위한 PyTorch 인터페이스를 제공하며, 계산 리소그래피 연구의 공개 벤치마크 기반이 된다.

## 주요 기여
1. PyTorch + GPU + FFT 기반 오픈소스 ILT 플랫폼 (전체 칩 병렬 처리)
2. ILT 흐름 모듈 분리: 시뮬레이션/초기화/최적화/평가 독립 교체 가능
3. AI 기반 ILT 방법 (Neural-ILT, DevelSet, ILILT 등) 통합 인터페이스
4. 계산 리소그래피 연구의 공개 벤치마크 플랫폼

## Recipe/Process Flow 상세

### OpenILT의 설계 원칙
```
기존 ILT 연구의 문제:
  독점 상용 툴: 재현 불가능, 코드 공개 불가
  각 연구 그룹: 자체 시뮬레이터 구현 → 중복, 비교 어려움
  재현성 부족: 방법 비교 시 공정한 기준 없음
  GPU 가속: 각 구현마다 다른 최적화 수준

OpenILT 목표:
  공개 플랫폼: 재현 가능한 ILT 연구 환경
  모듈식: 각 구성요소 독립 교체/확장
  GPU 가속: PyTorch + CUDA FFT 통합
  AI 통합: Neural-ILT, DevelSet 등 구현 표준 인터페이스
```

### 프레임워크 아키텍처
```
구성요소 분리 (Decoupled):

1. 리소그래피 시뮬레이션 모듈:
   Hopkins TCC 기반 광학 모델
   Abbe 비가간섭 모델
   레지스트 모델 (임계값 기반, 해석적)
   GPU CUDA FFT: 빠른 항공 이미지 계산
   미분 가능: autograd 통합 → 기울기 계산

2. 초기화 모듈:
   타겟 레이아웃 → 초기 마스크
   방법: 타겟 직접 사용, 팽창/수축 형태 연산
   ML 초기화: Neural-ILT, DevelSet 등 플러그인

3. 최적화 모듈:
   수치 ILT: 기울기 기반 (Adam, L-BFGS)
   AI ILT: 신경망 순방향 패스
   목적함수: L_EPE, L_PVB, L_MRC 모듈식

4. 평가 모듈:
   EPE, PV Band, 마스크 복잡도 계산
   표준 벤치마크: ICCAD 2013 패턴

Python/PyTorch 인터페이스:
  from openilt import LithoSimulator, ILTOptimizer
  sim = LithoSimulator(process_params)
  opt = ILTOptimizer(sim, method='gradient')
  mask = opt.optimize(target_layout)
```

### GPU 가속 및 병렬 처리
```
FFT 가속:
  항공 이미지 = IFFT(TCC × FFT(mask))
  CUDA FFT: 배치 FFT → 다수 클립 동시 처리
  속도: CPU 대비 수십~수백 배 빠름

전체 칩 병렬 처리:
  전체 칩 → 타일 분할 → GPU 배치 처리
  배치 크기: GPU 메모리 기반 자동 조정
  결과 수집: 병렬 처리 후 마스크 조립

AI 모델 통합:
  Neural-ILT, DevelSet, ILILT: OpenILT 시뮬레이터 사용
  → 공정한 비교 가능 (같은 광학 모델)
  → 새 AI 방법 쉬운 통합
```

### 벤치마크 및 재현성
```
공개 벤치마크:
  ICCAD 2013 패턴: 52개 표준 테스트 클립
  평가 지표: EPE, PV Band, 마스크 복잡도
  리더보드: 다양한 방법 비교 가능

지원 방법:
  수치 ILT: 기울기 기반, L-BFGS
  Neural-ILT: U-Net 기반 엔드투엔드
  DevelSet: 신경 레벨셋
  ILILT: 암묵적 학습
  A2-ILT: 어텐션 + RL

설치:
  pip install openilt
  GitHub: https://github.com/OpenOPC/OpenILT
```

## OPC 툴 구현 관련성
- **SKOPC ILT 백엔드**: `skopc/modeling/openilt_adapter.py`는 OpenILT를 백엔드로 직접 사용
- **공개 벤치마크**: SKOPC ILT 품질을 OpenILT ICCAD 2013 벤치마크로 평가
- **모듈 교체**: OpenILT 모듈식 구조로 광학 모델/최적화 알고리즘 쉬운 교체
- **AI 통합**: OpenILT 인터페이스로 Neural-ILT, DevelSet 등 AI 방법 SKOPC 통합

## 참고문헌
- ISEDA 2024, Xi'an, China
- GitHub: https://github.com/OpenOPC/OpenILT
- 저자 소속: CUHK (Bei Yu, Martin Wong 그룹)
- 관련: TorchLitho (SPIE 12954, 2024)
- 관련: Neural-ILT (ICCAD 2020 / TCAD 2022)
- 관련: DevelSet (ICCAD 2021 / TCAD 2023)

## 태그
`Recipe`, `ISEDA`, `ILT`, `OpenSource`, `Platform`, `PyTorch`, `GPU`, `FFT`, `Benchmark`, `MaskOptimization`, `CUHK`, `BeiYu`, `2024`
