# Data Efficient Lithography Modeling with Transfer Learning and Active Data Selection

## 메타데이터
- **저자**: Yibo Lin, Meng Li, Yuki Watanabe, Taiki Kimura, Tetsuaki Matsunawa, Shigeki Nojima, David Z. Pan
- **연도**: 2018
- **게재지/학회**: arXiv:1807.03257 (cs.LG / stat.ML), IEEE TCAD 게재
- **DOI/URL**: https://arxiv.org/abs/1807.03257
- **인용수**: 다수 인용 (리소그래피 머신러닝 핵심 논문)

## 핵심 요약
반도체 리소그래피 레지스트 모델링에서 학습 기반 방법의 데이터 효율성 문제를 해결하는 프레임워크를 제안한 논문. 구형 기술 노드의 기존 데이터를 전이 학습(Transfer Learning)으로 활용하고, 능동 학습(Active Learning)으로 타겟 노드의 핵심 데이터 포인트만 선별하여 3-10배의 훈련 데이터 절감을 달성한다.

## 주요 기여
- 기존 기술 노드 데이터를 신규 노드 레지스트 모델링에 재활용하는 전이 학습 프레임워크
- 정보량 최대화 기준 능동 데이터 선택으로 불필요한 데이터 수집 최소화
- 3-10배 훈련 데이터 절감 달성 (기존 방법과 동등한 정확도 유지)
- 접촉 레이어(contact layer) 패턴에 대한 레지스트 모델링 검증
- 비용 및 시간이 많이 드는 제조 실험 데이터 수집 부담 현저히 감소

## 알고리즘/수식
- **전이 학습 (Transfer Learning)**:
  - 소스 도메인: 구형 노드 (예: 28nm) 레지스트 데이터 D_source
  - 타겟 도메인: 신규 노드 (예: 14nm) D_target (소량)
  - 소스로 사전 훈련: θ₀ = argmin_{θ} L(f_θ, D_source)
  - 타겟으로 미세 조정: θ* = argmin_{θ} L(f_θ, D_target), 초기화 = θ₀

- **능동 학습 (Active Learning)**:
  - 초기 레이블 풀: D_labeled (소량)
  - 반복: 가장 정보가 많은 샘플 x* 선택 후 레이블 획득
  - 정보량 기준:
    - 불확실성 기반: x* = argmax_{x} H(f_θ(x))  (엔트로피 최대화)
    - 앙상블 불일치: x* = argmax_{x} Var[{f_θᵢ(x)}]
    - 최대 예측 변화: x* = argmax_{x} ||∇_{θ} f_θ(x)||

- **레지스트 모델 아키텍처**:
  - 입력: 에어리얼 이미지 강도 I_aerial(x,y) 타일
  - 출력: 레지스트 패턴 예측 (이진화 후)
  - CNN 기반: 컨볼루션 레이어 → 풀링 → FC 레이어

- **데이터 절감 실증**:
  - 기존 방법: N 샘플 필요
  - 전이 학습 단독: N/3 샘플
  - 전이 + 능동 학습: N/10 샘플 (동등 정확도)

## OPC 툴 구현 관련성
SKOPC의 `skopc/modeling/calibration.py` 모듈에서 공정 모델 캘리브레이션에 직접 활용. 신규 공정 노드(7nm, 5nm EUV)로 전환 시 기존 노드 데이터 재활용으로 캘리브레이션 비용 최소화. 능동 학습으로 측정 패턴 선택 최적화하여 물리 실험 횟수 절감. `TorchResist`와 연계하여 미분가능 레지스트 모델 파라미터 전이 학습 구현 가능.

## 참고문헌 (핵심)
- Settles, "Active Learning Literature Survey" (2010) — 능동 학습 종합
- Pan & Yang, "A Survey on Transfer Learning" (2010) — 전이 학습 종합
- Dill et al., 레지스트 모델 원전 (1975)
- Lin et al., VLSI 리소그래피 모델링 관련 ICCAD/DAC 논문들

## 태그
`lithography-modeling`, `transfer-learning`, `active-learning`, `resist-model`, `data-efficient`, `calibration`, `contact-layer`, `2018`, `arxiv`, `IEEE-TCAD`
