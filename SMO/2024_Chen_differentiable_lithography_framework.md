# Open-Source Differentiable Lithography Imaging Framework

## 메타데이터
- **저자**: Guojin Chen, Hao Geng, Bei Yu, David Z. Pan
- **연도**: 2024
- **게재지/학회**: SPIE 2024 (Accepted)
- **DOI/URL**: https://arxiv.org/abs/2409.15306
- **인용수**: 신규 논문

## 핵심 요약
반도체 리소그래피 시뮬레이션과 최적화를 위한 오픈소스 미분가능(differentiable) 프레임워크 TorchLitho를 소개하는 논문. GPU 연산 능력과 자동 미분(autodiff)을 결합하여 Abbe/Hopkins 이미징 모델, RET(Resolution Enhancement Technique) 최적화를 통합 지원한다. 반도체 제조 비용의 30-40%를 차지하는 리소그래피 공정 개선에 직접 기여하며, SMO를 포함한 다양한 최적화 작업을 단일 프레임워크로 처리한다.

## 주요 기여
- 리소그래피의 핵심 구성 요소를 미분가능 모듈로 모델링하는 통합 프레임워크 구축
- Abbe 이미징 모델과 Hopkins 이미징 모델(TCC 기반) 모두 구현 및 근사법 제공
- SMO, ILT, OPC 등 RET 최적화를 단일 자동미분 파이프라인으로 통합
- GPU 가속으로 대규모 레이아웃 시뮬레이션 효율화
- GitHub(TorchOPC/TorchLitho)에 완전 공개 — 오픈소스 기여

## 알고리즘/수식
- **Abbe 이미징 모델**: 비간섭 조명의 에어리얼 이미지 계산
  - I(x,y) = Σ_k |h_k * m(x,y)|², h_k: 부분간섭성 point spread function
- **Hopkins 이미징 모델 (TCC)**:
  - I(x,y) = ΣΣ TCC(f,g;f',g') · M(f,g) · M*(f',g')
  - TCC(f,g;f',g') = ∫∫ J(f'',g'') · H(f+f'',g+g'') · H*(f'+f'',g'+g'') df''dg''
- **미분가능 SMO**: adjoint back-propagation으로 소스 및 마스크 그래디언트 계산
- **자동 미분**: PyTorch autograd 활용, 전방향 패스 중간 상태 불필요

## OPC 툴 구현 관련성
SKOPC의 핵심 의존성인 TorchLitho의 소스 프레임워크와 직결. `skopc/modeling/litho_engine.py`의 LithoEngine이 이 프레임워크 위에서 동작. SMO 구현 시 `torch.autograd`로 소스 픽셀 그래디언트 직접 계산 가능. 특히 `skopc/smo/` 모듈의 gradient-based 최적화 루프에서 이 프레임워크의 `backward()` 메서드 활용 방식 참고 필수.

## 참고문헌 (핵심)
- Born & Wolf, "Principles of Optics" (Hopkins 모델 원전)
- Abbe, E. (1873) — Abbe 이미징 이론
- Mentor Graphics/SPIE TCC 관련 논문들
- TorchOPC GitHub repository

## 태그
`SMO`, `differentiable-lithography`, `TorchLitho`, `Abbe-model`, `Hopkins-model`, `TCC`, `GPU-acceleration`, `open-source`, `PyTorch`, `autodiff`, `RET`, `2024`, `SPIE`
