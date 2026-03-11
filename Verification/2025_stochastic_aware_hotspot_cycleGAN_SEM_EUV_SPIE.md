# Stochastic-Aware Hotspot Detection with CycleGAN-Augmented SEM Data and Uncertainty Quantification for EUV Process Control

## 메타데이터
- **저자**: (저자명 확인 필요 — SPIE Photomask Technology + EUV Lithography 2025 발표)
- **연도**: 2025
- **게재지/학회**: SPIE Photomask Technology + EUV Lithography 2025, Presentation #13686-56
- **DOI/URL**: https://spie.org/photomask-technology/presentation/Stochastic-aware-hotspot-detection-with-cycleGAN-augmented-SEM-data-and/13686-56
- **인용수**: 미확인 (2025년 최신 논문)

## 핵심 요약
EUV 리소그래피에서 확률적(stochastic) 결함 — 랜덤 브리징(random bridging), 콘택트 보이드(contact void) 등 — 에 특화된 핫스팟 검출 프레임워크를 제안한다. CycleGAN 기반 데이터 증강으로 SEM 이미지의 데이터 불균형 및 EUV 특유의 확률적 변동을 시뮬레이션하고, CNN 분류기에 불확실성 정량화(Uncertainty Quantification, UQ) 모듈을 결합하여 모델 신뢰도를 향상시킨다. 기존 CNN 대비 F1-score 17.8% 향상, CD 오차 편차 26.5% 감소를 달성하며, 실시간 OPC 피드백 및 공정 제어 시스템에 적용 가능한 적응형 제어 프레임워크를 제공한다.

## 주요 기여
- **CycleGAN 기반 SEM 데이터 증강**: EUV 확률적 변동을 반영한 합성 SEM 이미지 생성으로 데이터 불균형 해소
- **불확실성 정량화(UQ) 통합 CNN**: 검출 결과의 신뢰도 수치화 및 불확실한 예측의 위험 인식 모니터링
- **확률적 결함 특화 설계**: 랜덤 브리징, 콘택트 보이드 등 EUV 특유 결함 유형 최적화
- **실시간 OPC 피드백 지원**: 예측 불확실성을 실시간 OPC 및 공정 제어에 피드백
- **패턴 무관 성능**: 다양한 레이아웃 패턴 유형에서 일반화된 핫스팟 검출

## 검증 방법론
- **SEM 데이터셋 평가**: EUV 공정 SEM 이미지 데이터셋에서 핫스팟 검출 성능 평가
- **CycleGAN 증강 효과 절제 연구**: CycleGAN 증강 전후 검출 성능 비교
- **UQ 모듈 캘리브레이션**: 실험적 보정(empirical calibration)으로 불확실성 추정 정확도 검증
- **기존 CNN 비교**: 표준 CNN 분류기 대비 F1-score, CD 오차 편차 비교
- **다양한 패턴 일반화**: 여러 레이아웃 패턴 유형에서의 성능 일관성 측정

## 검증 지표
- **F1-score**: 핫스팟 검출 정밀도-재현율 조화 평균 (기존 CNN 대비 +17.8%)
- **CD 오차 편차**: Critical Dimension 오차의 표준편차 (기존 대비 -26.5%)
- **예측 불확실성 캘리브레이션**: UQ 모듈의 신뢰 구간 보정 정확도
- **False Positive Rate**: EUV 확률적 결함 특화 오탐률
- **사용 시뮬레이터**: EUV 리소그래피 SEM 이미지 데이터셋
- **검증 커버리지**: EUV 공정 SEM 데이터셋 (랜덤 브리징 + 콘택트 보이드 포함)

## OPC 툴 구현 관련성
SKOPC의 EUV OPC 검증 및 핫스팟 검출 모듈에 다음과 같이 활용 가능:
1. **EUV 확률적 결함 검출기**: SKOPC EUV OPC 파이프라인에 확률적 결함 특화 핫스팟 검출기 통합
2. **CycleGAN 데이터 증강**: EUV SEM 학습 데이터 부족 문제를 CycleGAN 합성 데이터로 해결
3. **불확실성 인식 OPC**: 핫스팟 검출 결과의 불확실성을 OPC 수정 우선순위 결정에 활용
4. **실시간 공정 제어 연동**: 예측 불확실성 기반 SKOPC 실시간 공정 제어 피드백 루프 구현
5. **고-NA EUV 확장성**: 불확실성 정량화 프레임워크로 고-NA EUV의 더 심각한 확률적 효과에 적응

## 참고문헌 (핵심)
- Zhu et al. (2017) - CycleGAN (Unpaired Image-to-Image Translation)
- Gal & Ghahramani (2016) - Dropout as Bayesian Approximation (불확실성 정량화)
- SPIE 2024 - Hotspot discovery and variability analysis for advanced EUV processes
- Siemens-imec (2025) - EUV 확률적 실패 저감 연구 (wafer 레벨 검증)
- ICCAD 2019 핫스팟 검출 벤치마크 데이터셋

## 태그
`Verification`, `Hotspot Detection`, `EUV`, `Stochastic`, `CycleGAN`, `Data Augmentation`, `Uncertainty Quantification`, `SEM`, `SPIE`, `2025`, `Process Control`, `CNN`, `Random Bridging`, `Contact Void`, `OPC Feedback`
