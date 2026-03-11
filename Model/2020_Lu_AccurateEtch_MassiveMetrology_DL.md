# Accurate Etch Modeling with Massive Metrology and Deep-Learning Technology

## 메타데이터
- **저자**: Yifei Lu et al. (ASML / MXP)
- **연도**: 2020
- **게재지**: Proc. SPIE 11327, Optical Microlithography XXXIII, 113270B
- **DOI/URL**: https://doi.org/10.1117/12.2552001

## 핵심 요약
ASML MXP 대규모 계측(AEI, After-Etch Inspection) 웨이퍼 데이터를 딥러닝 에치 모델(Newron Etch model)과 통합하여 에치 모델 정확도를 획기적으로 향상시킨다. MXP(CD+EP) + Newron 에치 모델 통합으로 기준 모델 대비 약 45% 예측 RMS 오차 감소를 달성한다.

## 주요 기여
1. ASML MXP 대규모 AEI 계측 데이터와 딥러닝 에치 모델(Newron) 통합
2. 기준 에치 모델 대비 45% 예측 RMS 오차 감소 달성
3. 에치 공정의 복잡한 근접 효과를 대용량 데이터로 학습하는 DL 접근법
4. 첨단 노드 에치 OPC 보정을 위한 정확하고 신뢰할 수 있는 에치 모델 제공
5. 대규모 계측(massive metrology) 인프라와 DL의 시너지 효과 실증

## 모델 수식/아키텍처
- **Newron DL 에치 모델**:
  - 입력: MXP 계측 데이터 (CD, EP — Edge Placement)
  - 딥러닝 아키텍처: 에치 패턴 의존성 학습
  - 출력: 에치 바이어스 예측 (post-etch CD 변화)
- MXP 데이터: 자동화 전자빔 계측(CD-SEM 다중 포인트) 기반 대규모 샘플링
- 통합 교정: DL 에치 모델을 OPC 리소그래피 모델과 순차 결합
- 검증: 테스트 게이지 RMS 오차로 모델 성능 평가

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드 (DL 에치 + 물리 리소그래피 모델 결합)

## OPC 툴 구현 관련성
- SKOPC 에치 모델 모듈에 DL 기반 Newron 에치 접근법 통합 방향 참조
- 대규모 AEI 계측 데이터 기반 DL 에치 모델의 산업 검증 사례
- `2020_Lu_MassiveMetrology_DeepLearning_Etch.md` (기존)와 동일 저자 계열 — 내용 중복 확인 필요
- ASML MXP + Newron 에치 솔루션의 구체적 구현 및 성능 데이터

## 태그
`Model`, `Etch`, `DeepLearning`, `MassiveMetrology`, `OPC`, `ASML`, `Newron`, `AEI`, `SPIE`
