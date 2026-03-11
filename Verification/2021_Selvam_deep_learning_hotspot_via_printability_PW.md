# Deep Learning-Based Hotspot Prediction of Via Printability in Process Window Corners

## 메타데이터
- **저자**: Punitha Selvam, Pouya Rezaeifakhr, Uwe Paul Schroeder, Janam Bakshi, Omnia Mohamed, Fadi Batarseh, Sriram Madhavan
- **연도**: 2021
- **게재지**: Proc. SPIE 11614, Design-Process-Technology Co-optimization XV, 116140X
- **DOI/URL**: https://doi.org/10.1117/12.2583662

## 핵심 요약
다층 공정에서 발생하는 복잡한 via 인쇄 약점(weak point)을 딥러닝으로 예측하는 방법론을 제안한 논문. 전통적인 규칙 기반 및 패턴 매칭 방식으로는 정의하기 어려운 다층 상호작용 기반 실패 모드를 딥러닝이 대용량 공정 데이터로부터 직접 학습하여, 공정 윈도우 코너 조건에서의 via 프린터빌리티 hotspot을 정확하게 예측하였다.

## 주요 기여
1. **다층 Via 프린터빌리티 딥러닝 예측**: 다층 레이아웃 상호작용을 고려한 via 인쇄 약점 예측 딥러닝 모델
2. **공정 윈도우 코너 조건 hotspot 포착**: 공정 변동 한계 조건(포커스/도즈 코너)에서의 via 인쇄 실패를 사전 예측
3. **복잡한 다층 상호작용 학습**: 전통적 패턴 매칭으로 정의 불가능한 다층 기반 실패 모드를 딥러닝이 데이터로부터 직접 학습
4. **대용량 공정 데이터 활용**: 다량의 실제 공정 데이터에서 추출한 특징으로 모델 훈련
5. **Via 레이어 특화**: via/contact 레이어의 프린터빌리티 예측에 특화된 딥러닝 아키텍처

## 검증 방법론
- 다층 레이아웃과 공정 윈도우 코너 시뮬레이션 데이터로 딥러닝 모델 훈련
- 공정 윈도우 코너 조건에서의 리소그래피 시뮬레이션 결과와 딥러닝 예측 비교
- Via 프린터빌리티 hotspot 포착률(recall)과 false positive 비율 평가
- 전통적 패턴 매칭 기반 hotspot 검출과 딥러닝 기반 검출의 성능 비교

## OPC 툴 구현 관련성
- SKOPC의 via/contact 레이어 OPC 검증 모듈에 딥러닝 기반 프린터빌리티 예측 추가 시 참조
- `2021_Kareem_PVB_ML_prediction.md`(기수집)의 PVB(Process Variation Band) ML 예측과 상보적: 이 논문은 via 레이어 특화 공정 윈도우 코너 hotspot 예측
- SKOPC의 다층 공정 상호작용 고려 OPC 검증 기능 설계의 기초 문헌
- `recipes/example_euv.yaml` EUV via/metal 레이어의 딥러닝 기반 공정 윈도우 검증 모듈 구현 시 참조

## 태그
`Verification`, `SPIE`, `Deep Learning`, `Hotspot`, `Via`, `Printability`, `Process Window`, `Multi-layer`, `OPC`
