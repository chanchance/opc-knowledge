# Machine Learning Models for Edge Placement Error Based Etch Bias

## 메타데이터
- **저자**: Yang Meng, Young-Chang Kim, Shujie Guo, Zhongli Shu, Yingchun Zhang, Qingwei Liu
- **연도**: 2021
- **게재지**: IEEE Transactions on Semiconductor Manufacturing, Vol. 34, pp. 42–48 (February 2021)
- **DOI/URL**: https://doi.org/10.1109/TSM.2020.3044041 | https://ieeexplore.ieee.org/document/9284482

## 핵심 요약
첨단 기술 노드에서 etch bias(식각 편차) 제어를 위해 EPE(Edge Placement Error) 기반 머신러닝 모델을 제안하고 실증한 논문. 단일 신경망(single NN), 앙상블 신경망(ensemble NN), 랜덤 포레스트(RF) 세 가지 ML 모델을 비교 평가하였으며, 웨이퍼 상에서 EPE를 대량으로 자동 측정하는 이미지 처리 기반 방법론도 함께 제시하였다.

## 주요 기여
1. **EPE 기반 ML etch bias 모델 3종 비교**: 단일 NN, 앙상블 NN, 랜덤 포레스트의 정확도·처리 시간 트레이드오프 정량 비교
2. **신규 피처 벡터(feature vector) 설계**: etch bias 예측 ML에 최적화된 레이아웃 피처 정의
3. **자동 대량 EPE 측정 방법론**: 이미지 처리 기반으로 웨이퍼 상 EPE를 대규모 자동 측정하는 방법 제안
4. **1D/2D 패턴 모두 검증**:
   - 1D: 절대 오차 ±2nm 이하, 평균 상대 오차 10% 이하
   - 2D: 평균 절대 오차 4nm 이하, 표준편차 3nm, 상대 오차 15% 이하
5. **업계 최신 기술 노드 실증**: 실제 양산 기술 노드 데이터로 검증

## 검증 방법론
- 이미지 처리 기반 자동 EPE 측정 시스템으로 웨이퍼 대량 데이터 수집
- 1D 패턴(L/S)과 2D 패턴(복잡한 레이아웃) 별도 검증
- 세 가지 ML 모델의 RMSE, 절대 오차, 상대 오차 비교
- 기존 rule-based 및 model-based etch bias 방식과 ML 방식의 정확도/속도 비교

## OPC 툴 구현 관련성
- SKOPC의 etch 보정 모듈(EPC, Etch Proximity Correction)에서 ML 기반 etch bias 모델 도입 시 핵심 참조
- `2022_Shi_deep_learning_etch_model_OPC_accuracy.md`, `2021_Hooker_ML_etch_model_OPC_ILT.md`와 함께 ML etch 모델 계보 형성
- 앙상블 NN과 랜덤 포레스트의 2D 패턴 처리 정확도 데이터는 SKOPC etch 모델 성능 벤치마크 기준으로 활용 가능
- 자동 EPE 측정 방법론은 OPC 검증 루프의 측정 자동화 설계에 직접 참조

## 태그
`Verification`, `IEEE`, `Etch Bias`, `EPE`, `Machine Learning`, `Neural Network`, `Random Forest`, `OPC`, `TSM`
