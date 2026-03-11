# Inverse Lithography Physics-informed Deep Neural Level Set for Mask Optimization

## 메타데이터
- **저자**: Xing-Yu Ma, Shaogang Hao
- **연도**: 2023
- **게재지/학회**: Applied Optics (2023), arXiv:2308.12299
- **DOI/URL**: https://arxiv.org/abs/2308.12299
- **인용수**: Applied Optics 게재

## 핵심 요약
딥러닝과 역리소그래피(ILT)를 결합한 ILDLS(Inverse Lithography Deep Level Set) 프레임워크 논문. 물리 기반 ILT를 딥러닝 레이어로 통합하여, 순수 ILT 대비 몇 자릿수(orders of magnitude) 계산 시간 단축과 동시에 프린터블리티(printability) 및 공정 윈도우(process window) 향상을 달성한다. 반복적인 마스크 예측과 보정(iterative mask prediction and correction)으로 품질을 점진적으로 개선한다.

## 주요 기여
- 물리 기반 ILT를 딥러닝 내부 레이어로 통합하는 하이브리드 아키텍처 (ILDLS)
- 기존 ILT 대비 수 자릿수 계산 시간 단축 달성
- 순수 딥러닝 방법 대비 인쇄 충실도(printability)와 공정 윈도우 모두 개선
- 반복적 마스크 예측+보정 루프를 통한 점진적 품질 향상
- 리소그래피 물리 지식을 DL 제약으로 활용하는 physics-informed 접근

## 알고리즘/수식
- **Level Set 표현**: 마스크를 이진 함수 대신 수준집합 함수(level set function) φ(x,y)로 표현
  - Mask(x,y) = H(φ(x,y)), H: Heaviside 함수
- **ILT 레이어**: 기존 ILT 최적화 단계를 미분가능 레이어로 구현
  - 마스크 그래디언트: ∂Loss/∂φ = ∂Loss/∂I · ∂I/∂φ
- **Physics-informed Loss**:
  ```
  L_total = L_EPE + λ₁·L_PV + λ₂·L_complexity
  ```
  - L_EPE: Edge Placement Error, L_PV: Process Variation, L_complexity: 마스크 복잡도
- **반복 보정**: 초기 DL 예측 → ILT 보정 → 재예측 루프

## OPC 툴 구현 관련성
SKOPC의 `skopc/modeling/` 모듈에서 ILT 구현 시 이 하이브리드 접근법 참고 가능. 특히 `openilt_adapter.py`가 OpenILT를 래핑하는 현재 구조에서, DL 기반 초기화 → ILT 정밀화 파이프라인으로 발전시키는 데 활용. Level set 표현은 GNN-OPC의 세그먼트 변위와 상보적으로 사용 가능.

## 참고문헌 (핵심)
- Osher & Sethian, "Fronts propagating with curvature-dependent speed" (level set 원전)
- Yang et al., GAN-OPC (GAN 기반 OPC)
- Chen et al., DAMO
- Geng et al., TorchOPC 관련

## 태그
`ILT`, `level-set`, `physics-informed`, `deep-learning`, `hybrid`, `mask-optimization`, `OPC`, `process-window`, `printability`, `2023`, `arxiv`, `Applied-Optics`
