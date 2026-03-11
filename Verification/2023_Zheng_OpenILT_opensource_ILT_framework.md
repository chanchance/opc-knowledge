# OpenILT: An Open Source Inverse Lithography Technique Framework

## 메타데이터
- **저자**: Su Zheng, Haoyu Yang, Bei Yu (CUHK, NVIDIA)
- **연도**: 2023
- **게재지/학회**: IEEE 15th International Conference on ASIC (ASICON 2023) — Invited Paper
- **DOI/URL**: https://ieeexplore.ieee.org/document/10396314/
- **GitHub**: https://github.com/OpenOPC/OpenILT
- **인용수**: 미확인

## 핵심 요약
OpenILT는 GPU 가속 및 AI 기반 ILT(역 리소그래피 기술) 방법의 신속한 개발과 평가를 지원하는 오픈소스 ILT 플랫폼이다. 리소그래피 시뮬레이션, 목적 함수, 평가 메트릭 등 다양한 ILT 컴포넌트를 통합하는 모듈형 유연 프레임워크를 제공하며, PyTorch와의 편리한 인터페이스로 GPU 가속 및 AI 기반 ILT 구현을 지원한다. 2023년 3월에 공개되었으며, Model-based OPC 확장(ModelOPC)을 포함하여 2024년에도 지속적으로 발전하고 있다.

## 주요 기여
- **모듈형 ILT 프레임워크**: 리소그래피 시뮬레이션, 목적 함수, 평가 메트릭의 모듈형 설계
- **PyTorch 인터페이스**: GPU 가속 및 AI 기반 ILT 구현을 위한 표준 딥러닝 인터페이스
- **GPU 가속 지원**: CUDA 기반 GPU 연산으로 고속 ILT 시뮬레이션
- **AI 방법 통합**: GAN-OPC, DAMO, Neural-ILT 등 기존 AI 기반 ILT 방법을 통일된 환경에서 재현
- **Model-based OPC 확장**: 2024년에 ModelOPC 확장으로 모델 기반 OPC까지 지원 범위 확대

## 검증 방법론
- **표준 ILT 벤치마크 평가**: ICCAD 2012/2019 벤치마크에서 ILT 성능 측정
- **GPU 가속 성능 벤치마크**: CPU 기반 ILT와 GPU 가속 ILT의 속도 비교
- **AI 방법 재현성 검증**: 기존 발표된 AI 방법들의 결과를 OpenILT 환경에서 재현
- **모듈 간 호환성 검증**: 다양한 리소그래피 모델, 목적 함수 조합으로 성능 측정
- **ModelOPC 검증**: 모델 기반 OPC 태스크에서의 EPE 수렴 및 정확도 측정

## 검증 지표
- **EPE 허용 범위**: EPE 위반 수 및 최대 EPE 기준 (ICCAD 벤치마크 설정)
- **PVB (Process Variation Band)**: 공정 변동에 대한 최적화 마스크 견고성
- **L2 오차**: 웨이퍼 시뮬레이션 이미지와 목표 이미지 간 L2 노름
- **Shots**: 마스크 복잡도 (제조 비용) 지표
- **사용 시뮬레이터**: OpenILT 내장 리소그래피 시뮬레이터 (Hopkins/Abbe 모델)
- **검증 커버리지**: ICCAD 2012 (28nm) 및 ICCAD 2019 벤치마크 패턴

## OPC 툴 구현 관련성
SKOPC의 ILT 및 모델 OPC 모듈에 직접 통합 또는 참조 가능:
1. **오픈소스 ILT 엔진**: OpenILT를 SKOPC의 ILT 모듈 참조 구현으로 활용
2. **PyTorch 기반 OPC**: OpenILT의 PyTorch 인터페이스를 SKOPC의 미분 가능 OPC에 통합
3. **벤치마크 재현**: OpenILT로 표준 ILT 벤치마크 결과를 재현하여 SKOPC 성능 비교
4. **ModelOPC 참조**: OpenILT의 ModelOPC 확장을 SKOPC의 모델 기반 OPC 구현 참고
5. **GPU 가속 패턴**: OpenILT의 CUDA 가속 리소그래피 시뮬레이션 구조를 SKOPC에 채택

## 참고문헌 (핵심)
- Yang et al. (2020) - GAN-OPC: GAN 기반 OPC 통합 대상
- Chen et al. (2021) - DAMO: UNet++ 기반 마스크 최적화 통합 대상
- Gu et al. (2022) - Neural-ILT: 신경망 기반 ILT 통합 대상
- Sun et al. (2023) - GPU-ILT: GPU 가속 수치 ILT 기준선
- PyTorch 프레임워크 (Paszke et al., 2019)

## 태그
`Verification`, `OPC`, `ILT`, `Open Source`, `Framework`, `PyTorch`, `GPU Acceleration`, `ASICON`, `2023`, `ModelOPC`, `Benchmark`, `ICCAD`
