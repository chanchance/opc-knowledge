# Keeping Deep Lithography Simulators Updated: Global-Local Shape-Based Novelty Detection and Active Learning

## 메타데이터
- **저자**: Hao-Chiang Shao, Hsing-Lei Ping, Kuo-shiuan Chen, Weng-Tai Su, Chia-Wen Lin, Shao-Yun Fang, Pin-Yian Tsai, Yan-Hsiu Liu
- **연도**: 2022
- **게재지/학회**: arXiv:2201.09717 (cs.CV)
- **DOI/URL**: https://arxiv.org/abs/2201.09717
- **인용수**: IEEE TCAD 관련 인용

## 핵심 요약
딥러닝 기반 제조 시뮬레이터를 지속적으로 최신 상태로 유지하기 위한 새로운 이상 탐지(novelty detection) 및 능동 학습 프레임워크를 제안한 논문. 기존 모델이 예측할 수 없는 "미학습 레이아웃 패턴"을 전역-로컬 이중 서브네트워크로 식별하고, 능동 학습으로 효율적인 추가 훈련 데이터를 선별 수집한다. 비용이 많이 드는 제조 검증 없이도 테스트 시 신규 레이아웃을 감지할 수 있는 것이 핵심 특징이다.

## 주요 기여
- 전역-로컬 이중 서브네트워크 기반 이상 탐지 (글로벌 구조 + 로컬 변형)
- 오토인코더로 전역 구조 이상도, 사전 훈련 모델로 로컬 변형 잠재 코드 추출
- 자기 어텐션(self-attention)으로 제조 유발 로컬 변형 감지 강화
- 2가지 능동 학습 샘플링 전략으로 대표 신규 레이아웃 선별
- 테스트 시 실측값(ground-truth) 없이도 이상 레이아웃 탐지 가능

## 알고리즘/수식
- **전역-로컬 이상도 점수**:
  ```
  S_novelty(x) = α · S_global(x) + (1-α) · S_local(x)
  ```
  - S_global(x) = ||x - Decoder(Encoder(x))||²  (오토인코더 재구성 오차)
  - S_local(x) = dist(z_pre(x), cluster_centers)  (사전 훈련 모델 잠재 코드)

- **자기 어텐션 강화**:
  - 로컬 변형 특징 맵에 Transformer self-attention 적용
  - A = softmax(QKᵀ/√d) · V (Q, K, V: 변형 특징에서 투영)

- **능동 학습 전략**:
  1. 불확실성 기반: 이상도 점수 상위 k개 선택
  2. 다양성 기반: 클러스터링 후 각 클러스터 대표 선택

- **시뮬레이터 업데이트 루프**:
  ```
  while 새 레이아웃 존재:
    S = compute_novelty(new_layouts)
    novel = filter(new_layouts, S > threshold)
    selected = active_sampling(novel)
    new_labels = fabricate_and_measure(selected)
    simulator = retrain(simulator, new_labels)
  ```

## OPC 툴 구현 관련성
SKOPC의 `LithoEngine` 지속 유지보수 및 공정 노드 전환에 직접 활용. 새로운 레이아웃 패턴이 기존 시뮬레이터의 훈련 분포 밖에 있는지 자동 감지하고, 필요한 최소 캘리브레이션 데이터만 수집하는 스마트 업데이트 워크플로우 구현 가능. 특히 고객사별 다양한 레이아웃 패턴을 처리할 때 `calibration.py`와 연동하여 적응형 시뮬레이터 유지 가능.

## 참고문헌 (핵심)
- 오토인코더 기반 이상 탐지: VAE 관련 논문들
- 능동 학습 종합: Settles (2010)
- Lin et al., 전이 학습 기반 리소그래피 모델링 (2018) — 관련 선행 연구
- LithoHoD (2024) — 같은 저자(Shao 등) 후속 연구

## 태그
`lithography-simulator`, `novelty-detection`, `active-learning`, `deep-learning`, `autoencoder`, `self-attention`, `simulator-update`, `2022`, `arxiv`
