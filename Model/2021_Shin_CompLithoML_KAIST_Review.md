# Computational Lithography Using Machine Learning Models

## 메타데이터
- **저자**: Youngsoo Shin (KAIST, School of Electrical Engineering)
- **연도**: 2021
- **게재지/학회**: IPSJ Transactions on System LSI Design Methodology, Vol. 14
- **DOI/URL**: https://doi.org/10.2197/ipsjtsldm.14.2; PDF: https://koasas.kaist.ac.kr/bitstream/10203/281048/1/117200.pdf
- **인용수**: 60+

## 핵심 요약
2010년 이후 계산 리소그래피의 광범위한 ML 응용을 체계적으로 정리한 KAIST 리뷰 논문. 마스크 최적화(OPC, EPC), 어시스트 피처 삽입, 리소그래피 모델링(광학 모델, 레지스트 모델), 테스트 패턴 선택, 핫스팟 감지/보정 등 계산 리소그래피의 전 영역에 걸친 ML 적용 현황을 포괄적으로 다룬다. 계산 비용이 높은 응용에서 학습된 모델이 빠른 결과 추정을 가능하게 한다는 핵심 장점을 강조한다.

## 주요 기여
- 계산 리소그래피 ML 응용의 2021년 기준 포괄적 리뷰
- OPC/EPC, SRAF, 리소그래피 모델링, 핫스팟 분야 체계적 분류
- ML이 계산 비용을 획기적으로 줄이는 메커니즘 분석
- 각 응용 분야의 ML 모델 아키텍처별 성능 비교
- 산업 적용 관점에서의 장단점 및 한계 분석

## 모델 아키텍처/수식
**ML 기반 계산 리소그래피 분류 체계:**

**1. 마스크 최적화 (OPC/EPC):**
```
Input: 레이아웃 패턴
ML Task: mask correction prediction
Models: CNN, GAN, RNN
Output: OPC/EPC 보정 마스크
```

**2. SRAF 삽입 및 검증:**
```
Input: 레이아웃 + 광학 이미지
ML Task: SRAF placement + printability check
Models: SVM, CNN, Random Forest
Output: SRAF 위치 + 프린팅 가능성 예측
```

**3. 리소그래피 모델링:**
광학 모델 ML 가속:
```
I_wafer ≈ CNN_θ(mask)   (전통 TCC 계산 대체)
속도: 전통 방법 대비 10~100×
```

레지스트 모델 ML 보강:
```
CD = DNN_θ(aerial_image_features)
     ↔ VTR/LPM의 ML 대안
```

**4. 테스트 패턴 선택 (Gauge Selection):**
```
Input: 전체 후보 게이지 패턴 D_all
ML Task: 대표 패턴 선택
Models: K-means, SVM, Gaussian Mixture
Output: 최적 보정 패턴 서브셋 D_sel
```
목표: |D_sel| << |D_all| 이면서 모델 정확도 유지

**5. 핫스팟 감지 (Hotspot Detection):**
```
Input: 레이아웃 + (선택적) 리소 시뮬레이션
ML Task: 이진 분류 (hotspot / non-hotspot)
Models: CNN, SVM, Ensemble
Output: 핫스팟 위치 + 확률
```

**6. 핫스팟 보정 (Hotspot Correction):**
```
Input: 핫스팟 레이아웃 영역
ML Task: 보정 패턴 생성
Models: Deep Generative (GAN, VAE)
Output: 보정된 레이아웃
```

**ML 모델 적합성 분석:**

| 응용 | 데이터 크기 | 추천 모델 | 정확도 |
|------|------------|-----------|--------|
| OPC/EPC | 대규모 | CNN, GAN | 높음 |
| SRAF | 중규모 | SVM, CNN | 중-높음 |
| 리소 모델링 | 대규모 | CNN, FNO | 높음 |
| 패턴 선택 | 소규모 | K-means | 중간 |
| 핫스팟 감지 | 대규모 | CNN | 높음 |

**계산 비용 절감 (대표 사례):**
```
OPC iteration time:
  Traditional: 수 분/타일
  ML-assisted: 수 초/타일 (100× 이상)

Hotspot detection:
  SPICE simulation: 수 시간
  ML prediction: 수 초 (10,000× 이상)
```

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 ML 기반 기능 개발 방향 설정에 중요한 참조. 리뷰에서 제시한 분류 체계를 따라 SKOPC의 각 모듈(OPC, SRAF, 리소 모델링, 핫스팟)에 ML을 순차적으로 통합할 수 있다. 특히 테스트 패턴 선택(gauge selection) ML은 SKOPC 보정 데이터 수집 비용 절감에 즉시 적용 가능. KAIST의 실습 레시피(practical recipes) 논문도 함께 참조 추천.

## 참고문헌 (핵심)
- Yang, H. et al., "GAN-OPC," DAC 2018
- Ye, C. et al., "LithoGAN," DAC 2019
- Chen, G. et al., "DAMO," ICCAD 2020
- Lin, Y. et al., "Data efficient lithography modeling with ResNet," ISPD 2018
- Shin, Y., "ML for computational lithography: practical recipes," VLSI (2025)

## 태그
`Model`, `OPC`, `MachineLearning`, `Review`, `KAIST`, `OPC_EPC`, `SRAF`, `LithographyModeling`, `HotspotDetection`, `GaugeSelection`, `CNN`, `GAN`, `SVM`, `ComputationalLithography`
