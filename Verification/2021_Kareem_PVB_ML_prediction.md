# Fast Prediction of Process Variation Band Through Machine Learning Models

## 메타데이터
- **저자**: Pervaiz Kareem, Yonghwi Kwon, Gangmin Cho, Youngsoo Shin
- **연도**: 2021
- **게재지**: Proc. SPIE 11613, Optical Microlithography XXXIV, 1161306
- **DOI/URL**: https://doi.org/10.1117/12.2583805
- **인용수**: 다수 (PVB ML 예측 분야 주요 논문)

## 핵심 요약
PVB(Process Variation Band)는 수율 추정, 핫스팟 검출, 마스크 최적화 등 여러 리소그래피 응용에 필수적이나, 기존 리소그래피 시뮬레이션은 속도가 매우 느려 칩의 일부에만 적용 가능했다. 본 논문은 cGAN(conditional Generative Adversarial Network) 등 ML 모델을 이용해 고속·충분한 정확도로 PVB를 예측하는 방법을 탐구한다. 제안 방법은 98% 이상의 패턴에서 평균 86% 정확도와 500배 속도 향상을 달성한다.

## 주요 기여
1. cGAN 기반 PVB 예측 모델 — 리고러스 시뮬레이션 대비 500배 속도 향상
2. 98% 패턴 커버리지, 평균 86% 예측 정확도 달성
3. 전칩 PVB 계산 가능성 제시 — 기존 소규모 계산의 근본적 한계 극복
4. 수율 추정·핫스팟 검출·마스크 최적화에 PVB를 실시간으로 활용하는 경로 개척

## 검증 방법론
- **PVB 정의**: 공정 윈도우(포커스·노광량 변동) 전체에서 웨이퍼 컨투어가 점유하는 공간적 범위
- **cGAN 모델**: 레이아웃 이미지를 입력받아 PVB 이미지를 직접 생성하는 조건부 생성 모델
- **비교 기준(Ground Truth)**: 리고러스 리소그래피 시뮬레이션으로 계산한 PVB
- **평가 지표**:
  - 예측 정확도: 86% 평균 (PVB 픽셀 단위 일치율)
  - 패턴 커버리지: 98% 이상 (예측 실패 패턴 2% 미만)
  - 속도: 리고러스 시뮬레이션 대비 500배 향상
- **훈련 데이터**: 다양한 피치·패턴 유형의 레이아웃 세그먼트

## 검증 지표
- EPE 허용 범위: PVB 내 최악 조건 컨투어의 설계 타겟 대비 오차
- 시뮬레이터: cGAN ML 모델 (리고러스 시뮬레이터로 레이블링된 훈련 데이터)
- 커버리지: 98% 패턴 커버리지 (전칩 적용 가능 수준)

## OPC 툴 구현 관련성
- **PVB 기반 OPC 검증 가속화**: `VerificationEngine`의 공정 윈도우 검사를 ML 예측으로 대체하여 TAT 극적 단축 가능
- PVB 계산을 전칩으로 확장하여 핫스팟 검출 커버리지 향상 — 기존 방법의 근본적 속도 장벽 해결
- cGAN 아키텍처는 레이아웃 이미지 기반 입출력 구조로 기존 OPC 플로우에 통합 용이
- 수율 추정 모듈과 OPC 검증 모듈을 ML PVB 예측으로 연결하는 아키텍처 구현의 기반

## 참고문헌
- SPIE Optical Microlithography XXXIV 2021, Vol. 11613
- 후속 연구: Fast and accurate prediction of PVB with custom kernels (SPIE 2023, Vol. 12495)

## 태그
`Verification`, `SPIE`, `PVB`, `ProcessVariationBand`, `MachineLearning`, `cGAN`, `Hotspot`, `YieldEstimation`, `FullChip`, `SpeedUp`
