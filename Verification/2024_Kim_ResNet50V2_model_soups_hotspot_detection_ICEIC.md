# Methodology for Lithography Hotspot Detection Using ResNet50V2 and Model Soups

## 메타데이터
- **저자**: Su Min Kim, Jae Wook Jeon
- **연도**: 2024
- **게재지**: 2024 International Conference on Electronics, Information, and Communication (ICEIC 2024)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10457195/

## 핵심 요약
리소그래피 핫스팟 탐지에 ResNet50V2와 모델 수프(model soups) 기법을 결합한 효율적 방법론을 제시한다. 클래스 불균형 문제를 해결하기 위해 기하학적 정보를 보존하면서 데이터를 재균형화하는 데이터 증강 기법을 도입하고, 모델 수프를 통해 여러 파인튜닝된 모델의 가중치를 평균화하여 성능을 향상시킨다. ICCAD-2012 벤치마크에서 평균 정밀도 0.908, F1 점수 0.926을 달성했다.

## 주요 기여
1. **ResNet50V2 + Model Soups** 조합의 리소그래피 핫스팟 탐지 방법론
2. 클래스 불균형 해결을 위한 기하학적 정보 보존 데이터 증강 전략
3. 여러 파인튜닝 모델의 가중치 평균화(model soups)로 성능 향상
4. ICCAD-2012 벤치마크에서 경쟁력 있는 성능 달성 (AP=0.908, F1=0.926)
5. 전이학습(transfer learning) 기반 핫스팟 탐지의 데이터 효율성 향상

## 검증 방법론
- **벤치마크 데이터셋**: ICCAD-2012 핫스팟 탐지 표준 벤치마크
- **기반 모델**: ResNet50V2 (ImageNet 사전훈련 → 파인튜닝)
- **앙상블 방법**: Model Soups - 여러 파인튜닝 모델의 가중치 평균화
- **데이터 전처리**: 클래스 불균형 보정 + 기하학적 정보 보존 증강
- **평가 지표**: 평균 정밀도(AP) = 0.908, F1 점수 = 0.926
- **비교**: ICCAD-2012 벤치마크 기존 방법 대비

## OPC 툴 구현 관련성
- ResNet50V2 기반 핫스팟 탐지를 OPC 후 검증 파이프라인에 통합하는 방법
- 클래스 불균형이 심한 핫스팟 데이터셋 학습 시 모델 수프 앙상블 전략 적용
- 사전훈련 모델의 전이학습을 활용한 소량 데이터 기반 OPC 핫스팟 분류기 구축
- 데이터 증강으로 리소그래피 핫스팟 탐지 모델의 일반화 성능 향상 방법

## 태그
`Verification`, `Hotspot`, `DeepLearning`, `ResNet`, `ModelSoups`, `DataAugmentation`, `ClassImbalance`, `ICEIC`, `IEEE`, `2024`
