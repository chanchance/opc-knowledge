# Machine Learning Techniques for OPC Improvement at the Sub-5nm Node

## 메타데이터
- **저자**: Changsoo Kim, Seungjong Lee, Sangwoo Park, No-Young Chung, Jungmin Kim, Narae Bang, Sanghwa Lee, SooRyong Lee, Robert Boone, Pengcheng Li, Jiyoon Chang, Xinxin Zhou, YoungMi Kim, MinSu Oh, Minsung Kim, Rachit Gupta, Jun Ye, Stanislas Baron
- **연도**: 2020
- **게재지**: Proc. SPIE 11323, Extreme Ultraviolet (EUV) Lithography XI, 1132317
- **DOI/URL**: https://doi.org/10.1117/12.2551841

## 핵심 요약
sub-5nm 노드 OPC 개선을 위한 머신러닝 기법을 연구한다. ASML-Brion의 Newron ML 제품군을 활용하여, ML 기반 보정 예측(OPC 가속)과 ML 레지스트 모델(정확도 향상) 두 가지 측면에서 기존 방법 대비 성능 향상을 벤치마크한다.

## 주요 기여
1. **ML 기반 OPC 보정 예측**: Newron 제품군의 ML 보정 예측으로 런타임 30%+ 단축
2. **ML 레지스트 모델**: 기존 리소그래피 모델 대비 시뮬레이션 정확도 15% 향상
3. **Sub-5nm EUV 적용**: 최첨단 EUV 노드에서 ML 기법의 실용적 검증
4. **패턴 충실도 유지**: 런타임 단축에도 불구하고 패턴 충실도 동등 수준 유지
5. **삼성-ASML-Brion 협력**: 파운드리-장비업체-소프트웨어 업체 공동 검증

## Recipe/Flow 상세
- **ML 기반 OPC 개선 플로우**:
  1. **ML 레지스트 모델 캘리브레이션**:
     - SEM 데이터로 기존 물리 모델 대신 ML 모델 학습
     - 입력: 광학 이미지 특징
     - 출력: 레지스트 윤곽 CD 예측
     - 정확도: 기존 모델 대비 15% 향상 (residual 감소)
  2. **ML 보정 예측 (Newron correction)**:
     - 기존 iterative OPC 대신 ML로 보정량 직접 예측
     - 입력: 레이아웃 특징 + 현재 마스크 형상
     - 출력: 각 fragment의 이동량 예측
     - 런타임: 기존 대비 30%+ 단축
  3. **하이브리드 플로우**:
     - ML 예측 → 초기 보정 적용
     - 물리 시뮬레이션으로 검증 및 fine-tuning
  4. **벤치마크 검증**:
     - Sub-5nm EUV 레이아웃에서 ML vs. 기존 OPC 비교
     - EPE, CDU, 런타임 지표 측정
- **Sub-5nm 특화 고려사항**:
  - EUV stochastic 효과 → ML 모델의 확률론적 거동 캡처
  - 극소 패턴 크기 → 높은 모델 정확도 요구
  - 대규모 데이터 학습 → 제품 레이아웃 다양성 필요

## OPC 툴 구현 관련성
- SKOPC GNN-OPC 모듈과 유사한 ML 기반 보정 예측 접근법
- ML 레지스트 모델 구현 참고 (`ml_resist_model.py`)
- 30%+ 런타임 단축 전략: ML 예측 + 물리 검증 하이브리드
- Sub-5nm EUV OPC 정확도 요구사항 이해

## 태그
`MachineLearning`, `OPC`, `Sub5nm`, `EUV`, `Newron`, `ResistModel`, `Runtime`, `SPIE`, `2020`
