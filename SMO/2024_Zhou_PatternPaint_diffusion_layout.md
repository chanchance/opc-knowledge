# PatternPaint: Practical Layout Pattern Generation Using Diffusion-Based Inpainting

## 메타데이터
- **저자**: Guanglei Zhou, Bhargav Korrapati, Gaurav Rajavendra Reddy, Chen-Chia Chang, Jingyu Pan, Jiang Hu, Yiran Chen, Dipto G. Thakurta
- **연도**: 2024 (DAC 2025 게재)
- **게재지/학회**: DAC 2025 (Design Automation Conference), arXiv:2409.01348
- **DOI/URL**: https://arxiv.org/abs/2409.01348
- **인용수**: DAC 2025 게재

## 핵심 요약
신규 기술 노드 개발 시 대규모 데이터셋 없이도 합법적인 레이아웃 패턴을 생성하는 PatternPaint 프레임워크를 제안한 논문. 사전 훈련된 이미지 기반 모델에 단 20개 DRC 준수 샘플로 퓨샷(few-shot) 미세 조정하고, 템플릿 기반 디노이징 방식으로 복잡한 인페인팅(inpainting)을 수행한다. Intel 18A(sub-3nm) 기술 노드에서 복잡한 2D 금속 배선 설계 규칙을 준수하는 패턴을 유일하게 생성 가능한 방법임을 실증한다.

## 주요 기여
- 사전 훈련 이미지 기반 모델에 단 20개 샘플 퓨샷 미세 조정으로 신기술 노드 적응
- 템플릿 기반 디노이징 방식으로 복잡한 레이아웃 인페인팅 수행
- 솔버 기반 합법화 없이 픽셀 수준에서 직접 DRC 준수 패턴 생성
- Intel 18A(sub-3nm) 2D 금속 배선에서 유일하게 합법적 패턴 생성 성공
- 기존 사전 훈련 모델 대비 1.87배 합법성 향상

## 알고리즘/수식
- **확산 기반 인페인팅**:
  - 기반 모델: 사전 훈련 이미지 확산 모델 (Stable Diffusion 계열)
  - 인페인팅: 레이아웃의 일부를 마스킹 후 DRC 준수 패턴으로 채움
  - x_0 ~ p_θ(x_0 | x_masked, context)

- **템플릿 기반 디노이징**:
  - 템플릿 T: DRC 준수 패턴의 구조적 틀 제공
  - 디노이징 시 T 조건부: x_{t-1} = f_θ(x_t, T, t)
  - 설계 규칙 정보를 컨디셔닝으로 주입

- **퓨샷 미세 조정**:
  - N=20 DRC 준수 샘플로 기반 모델 파인튜닝
  - LoRA(Low-Rank Adaptation) 또는 텍스트 인버전 기법 활용
  - 기술 노드별 새 DRC 패턴 학습 최소화

- **합법성 평가**:
  - 생성 패턴 → DRC 검사기 통과 비율 측정
  - 다양성 점수: 생성 패턴 집합의 커버리지

## OPC 툴 구현 관련성
SKOPC의 테스트 데이터 및 훈련 데이터 생성에 직접 활용 가능. `tests/fixtures/make_test_gds.py`의 테스트 레이아웃 생성을 PatternPaint 방식으로 확장하여 다양하고 현실적인 DRC 준수 테스트 패턴 자동 생성 가능. GNN-OPC 훈련 데이터 부족 문제를 퓨샷 패턴 생성으로 해결. 신규 공정 노드 지원 시 해당 노드의 소량 패턴으로 훈련 데이터 자동 생성 워크플로우 구축 가능.

## 참고문헌 (핵심)
- Ho et al., DDPM (2020) — 확산 모델 기반
- Rombach et al., "Latent Diffusion Models" (2022) — Stable Diffusion 기반
- Wang et al., DiffPattern (DAC 2023) — 관련 이산 확산 기반 패턴 생성
- Intel 18A 기술 노드 관련 문헌

## 태그
`layout-generation`, `diffusion-model`, `inpainting`, `few-shot`, `design-rules`, `DRC`, `sub-3nm`, `Intel-18A`, `DAC`, `2024`, `arxiv`
