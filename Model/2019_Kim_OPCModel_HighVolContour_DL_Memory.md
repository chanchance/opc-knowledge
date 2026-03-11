# OPC Model Accuracy Study Using High Volume Contour Based Gauges and Deep Learning on Memory Device

## 메타데이터
- **저자**: Young-Seok Kim, SeIl Lee, Zhenyu Hou et al. (Samsung / KLA)
- **연도**: 2019
- **게재지**: Proc. SPIE 10959, Metrology, Inspection, and Process Control for Microlithography XXXIII, 1095913
- **DOI/URL**: https://doi.org/10.1117/12.2515274

## 핵심 요약
고속 e-beam 장비(eP5)와 계측 처리 소프트웨어(MXP)로 생성한 10,000개 이상의 컨투어 기반 엣지 배치 게이지(EPG)와 딥러닝을 활용하여 메모리 소자의 OPC 모델 정확도를 향상시킨다. 기존 접근 대비 검증 게이지 1,400개 이상에서 47% 이상 모델 정확도 개선을 달성한다.

## 주요 기여
1. e-beam(eP5) + MXP로 10,000개 이상 컨투어 기반 EPG 고속 생성
2. 딥러닝과 물리 가이던스 모델 결합으로 정규화 달성
3. 검증 게이지 1,400개 이상에서 기존 대비 47% 이상 모델 정확도 향상
4. 메모리 소자 실칩 패턴에서의 성능 검증
5. 대용량 컨투어 게이지와 DNN의 결합이 OPC 모델 교정에 미치는 영향 정량화

## 모델 수식/아키텍처
- **DNN + 물리 가이던스 모델**:
  - 입력: 컨투어 기반 EPG (레이아웃 패치 + 계측 결과)
  - DNN: 여러 은닉층, 물리 모델 예측을 정규화(regularization)에 활용
  - 출력: CD/EPE 예측값
- 물리 가이던스: 기존 OPC 컴팩트 모델 예측을 DNN 학습의 앵커로 사용
- 게이지 생성: eP5 e-beam → MXP 컨투어 추출 → 자동 EPG 생성
- 교정: 10K+ 게이지로 학습, 1.4K 검증 게이지로 평가

## 모델 유형
- [x] 광학
- [x] 레지스트
- [x] ML/DL
- [x] 하이브리드 (물리 모델 정규화 + DNN)

## OPC 툴 구현 관련성
- SKOPC 모델 교정 파이프라인에서 대용량 e-beam 컨투어 데이터 활용 방향
- 물리 가이던스 DNN의 OPC 컴팩트 모델 대체/보완 구조 참조
- 메모리 소자 특화 OPC 모델 정확도 향상의 실증 사례
- `2019_Kim_MetrologyDL_OPCAccuracy.md`와 동일 저자/연도 — 다른 DOI로 별개 논문

## 태그
`Model`, `OPC`, `Calibration`, `DeepLearning`, `Contour`, `EPG`, `Memory`, `MassiveMetrology`, `eBeam`, `SPIE`
