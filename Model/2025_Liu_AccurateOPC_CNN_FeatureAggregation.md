# Accurate Optical Proximity Correction Using Convolutional Neural Network with Feature Aggregation

## 메타데이터
- **저자**: Yongkang Liu, Wei Zhao, Xulin Zhang, Yucheng Ji, Ruixiang Yan, Yuandong Gu
- **연도**: 2025
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 24, No. 2, 023201
- **DOI/URL**: https://doi.org/10.1117/1.JMM.24.2.023201

## 핵심 요약
FFT 컨볼루션 모듈과 기존 컨볼루션 모듈을 결합한 향상된 컨볼루션 블록(enhanced convolutional block)을 백본 네트워크에 도입하여 OPC 정확도를 개선하는 CNN 기반 방법을 제안한다. 특징 집계(feature aggregation) 기법으로 다중 스케일 패턴 특성을 효과적으로 포착한다.

## 주요 기여
1. FFT 컨볼루션 + 기존 컨볼루션 결합의 향상된 컨볼루션 블록 설계
2. 특징 집계(feature aggregation)로 다중 스케일 레이아웃 특성 포착
3. 기존 CNN OPC 대비 향상된 마스크 예측 정확도
4. OPC 수렴 속도 및 최종 EPE 성능 개선
5. JMM 저널 발표 — 최신(2025) CNN 기반 OPC 연구

## 모델 수식/아키텍처
- **향상된 컨볼루션 블록**:
  - FFT 컨볼루션: 주파수 영역에서 글로벌 수용 영역 포착
  - 기존 컨볼루션: 국소 공간 특징 추출
  - 병렬 결합: output = FFT_conv(x) + Conv(x)
- **특징 집계**: 다양한 수용 영역 크기의 특징 맵을 채널 방향으로 연결
- 백본 네트워크: U-Net 계열 또는 ResNet 계열 인코더-디코더
- 입력: 타겟 레이아웃 패치 → 출력: OPC 마스크 패치

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [x] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC CNN 기반 OPC 모듈에서 FFT 컨볼루션 통합 방향 제시
- 글로벌(FFT) + 국소(Conv) 특징 결합으로 장거리 및 단거리 OPC 효과 동시 포착
- `2021_Chi_SpeedupOPC_ML_IBM.md` 등 ML OPC 연구 계열의 2025년 정확도 개선
- TorchLitho 기반 미분 가능 리소그래피와 결합한 end-to-end OPC 학습 가능

## 태그
`Model`, `OPC`, `CNN`, `FFT`, `FeatureAggregation`, `MaskOptimization`, `DeepLearning`, `JMM`, `SPIE`
