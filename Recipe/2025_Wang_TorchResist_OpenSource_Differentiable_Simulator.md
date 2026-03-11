# TorchResist: Open-Source Differentiable Resist Simulator

## 메타데이터
- **저자**: Zixiao Wang, Jieya Zhou, Su Zheng, Shuo Yin, Kaichao Liang, Shoubo Hu, Xiao Chen, Bei Yu
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134251S
- **DOI/URL**: https://doi.org/10.1117/12.3062763
- **코드**: https://github.com/ShiningSord/TorchResist

## 핵심 요약
오픈소스 미분 가능(differentiable) 레지스트 시뮬레이터 TorchResist를 제안한다. 해석적(analytical) 접근법으로 레지스트 공정을 모델링하며, 최대 20개의 해석 가능한 파라미터를 가진 화이트박스(white-box) 시스템이다. 미분 가능 프로그래밍과 GPU 병렬 컴퓨팅을 활용하여 OPC, ILT 등 다른 컴퓨터 리소그래피 도구와의 공동 최적화(co-optimization)를 가능하게 한다.

## 주요 기여
1. **오픈소스 미분 가능 레지스트 시뮬레이터**: PyTorch 기반 완전 미분 가능 레지스트 모델 공개
2. **해석적 화이트박스 모델**: 블랙박스 ML 모델 대신 물리 기반 해석적 파라미터화로 해석 가능성 확보
3. **GPU 가속**: 병렬 컴퓨팅으로 기존 순차 시뮬레이터 대비 고속 연산
4. **OPC/ILT 공동 최적화**: 미분 가능성을 이용한 엔드-투-엔드 그래디언트 기반 최적화
5. **20개 해석 가능 파라미터**: 물리적 의미를 가진 소수의 파라미터로 레지스트 거동 포괄적 모델링

## Recipe/Flow 상세
- **TorchResist 구조 및 사용 플로우**:
  1. **레지스트 물리 모델**:
     - 노광(Exposure): 광학 이미지 → 레지스트 내 광자 흡수 분포
     - PEB(Post-Exposure-Bake): 산 확산(acid diffusion) 모델
     - 현상(Development): 현상 속도 모델 (Mack 모델 또는 변형)
     - 각 단계 해석적 수식화 → 미분 가능
  2. **PyTorch 구현**:
     - 모든 연산을 PyTorch 텐서 연산으로 구현
     - 자동 미분(autograd)으로 파라미터 그래디언트 계산
     - GPU(CUDA) 가속 지원
  3. **파라미터 캘리브레이션**:
     - 그래디언트 기반 최적화로 SEM 측정 데이터에 피팅
     - 20개 이하의 물리적 의미 있는 파라미터 최적화
     - 기존 방법 대비 빠른 캘리브레이션
  4. **OPC/ILT 공동 최적화**:
     - 광학 시뮬레이터(OpenILT 등)와 TorchResist 연결
     - 광학+레지스트 통합 파이프라인 미분 가능
     - 마스크 형상 → 광학 이미지 → 레지스트 패턴의 엔드-투-엔드 역전파
     - ILT: TorchResist 출력을 비용 함수로 마스크 최적화
  5. **검증**:
     - 다양한 노드 및 레이어에서 시뮬레이션 정확도 검증
     - 기존 상용 레지스트 시뮬레이터와 비교
- **오픈소스 의의**:
  - 학계 연구자가 레지스트 모델을 커스터마이징하고 OPC/ILT에 통합 가능
  - 재현 가능한 연구 환경 제공
  - 컴퓨터 리소그래피 교육 및 프로토타이핑 도구

## OPC 툴 구현 관련성
- SKOPC 레지스트 모델을 TorchResist로 대체 또는 병행 사용 가능
- `torch_resist_wrapper.py`: TorchResist를 SKOPC 파이프라인에 통합하는 래퍼
- 엔드-투-엔드 미분 가능 OPC/ILT 공동 최적화 구현
- 오픈소스 코드로 레지스트 파라미터 커스터마이징 및 새 모델 프로토타이핑

## 태그
`TorchResist`, `ResistSimulator`, `OpenSource`, `Differentiable`, `OPC`, `ILT`, `MachineLearning`, `PyTorch`, `GPU`, `CoOptimization`, `SPIE`, `2025`
