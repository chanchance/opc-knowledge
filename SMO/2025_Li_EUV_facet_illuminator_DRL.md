# Design of an All-Facet Illuminator for High NA EUV Lithography Based on Deep Reinforcement Learning

## 메타데이터
- **저자**: Tong Li, Yuqing Chen, Yanqiu Li, Lihui Liu
- **연도**: 2025
- **게재지/학회**: arXiv:2506.15558
- **DOI/URL**: https://arxiv.org/abs/2506.15558
- **인용수**: 신규 논문

## 핵심 요약
0.55 NA 고해상도 EUV 리소그래피 노광 장비용 전면 패싯(all-facet) 조명기를 설계한 논문. 기존 릴레이 광학계를 제거하여 광투과율을 35% 이상으로 높이고, 심층 강화학습(Deep RL)으로 이중 패싯(double facets) 매칭을 최적화하여 다양한 조명 퍼필 형상에서 99% 이상의 균일도를 달성한다. EUV 소스 최적화의 하드웨어 구현 관점을 제시하는 중요 논문.

## 주요 기여
- 릴레이 시스템 없는 전면 패싯 조명기 설계 방법론 (행렬 광학 기반)
- 심층 강화학습 기반 이중 패싯 매칭 알고리즘 (단일 요소 방법의 한계 극복)
- 향상된 학습 능력과 계산 효율을 갖춘 정책 네트워크(policy network) 설계
- 빠른 수렴을 제공하는 강화 신호(reward function) 설계
- 다중 조명 퍼필 형상 동시 최적화 지원

## 알고리즘/수식
- **행렬 광학 설계**: 패싯 배열 좌표 및 크기 계산
  - 출사 퍼필을 픽셀화(pixelated)하여 각 퍼필 패싯 미러의 좌표/크기 결정
- **심층 강화학습 프레임워크**:
  - 상태(State): 현재 패싯 배치 및 균일도 측정값
  - 행동(Action): 패싯 미러 위치/각도 조정
  - 보상(Reward): 투과율 × 균일도 복합 지표
  - 정책 네트워크: 향상된 학습 속도를 위한 커스텀 아키텍처
- **픽셀화된 소스 표현**:
  - 조명 소스를 2D 픽셀 그리드로 표현
  - 각 픽셀 = 독립적으로 제어 가능한 강도(intensity)
- **성능 지표**:
  - 투과율: T > 35%
  - 균일도: U > 99%
  - NA: 0.55 (High-NA EUV)

## OPC 툴 구현 관련성
SKOPC의 SMO 모듈에서 EUV 소스 최적화 구현 시 참고. 픽셀화된 EUV 소스 표현 방식은 `skopc/smo/` 내 소스 파라미터화에 직접 활용. 강화학습 기반 소스 최적화는 기존 그래디언트 기반 방법의 대안으로 고려 가능. High-NA EUV(0.55 NA) 지원 시 이 논문의 패싯 모델 참고.

## 참고문헌 (핵심)
- ASML 관련 EUV 조명 시스템 특허 및 논문
- Finders et al., "Illumination source optimization in EUV lithography," SPIE (2018)
- Deep RL 관련: PPO, DDPG 원전 논문들

## 태그
`EUV`, `SMO`, `illuminator-design`, `all-facet`, `high-NA`, `deep-reinforcement-learning`, `pixelated-source`, `0.55NA`, `uniformity`, `2025`, `arxiv`
