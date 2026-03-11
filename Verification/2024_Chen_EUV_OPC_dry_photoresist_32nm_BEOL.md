# EUV OPC Modeling of Dry Photoresist System for Pitch 32nm BEOL

## 메타데이터
- **저자**: Jyun-Ming Chen, David Rio, Maxence Delorme, Cyrus Tabery, Christoph Hennerkes, Chris Spence, Benjamin Kam, Mohand Brouri, Nader Shamma
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530C
- **DOI/URL**: https://doi.org/10.1117/12.3010402

## 핵심 요약
피치 32nm BEOL 금속 레이어에서 건식 포토레지스트 시스템의 EUV OPC 모델 정확도를 정량화하고 특성화한 논문. ASML Tachyon 소프트웨어를 이용한 ADI OPC 모델 캘리브레이션을 수행하고, 물리 기반 모델(Tachyon FEM+)과 머신러닝 기반 모델(Newron) 두 엔진의 정확도를 비교 평가하였다.

## 주요 기여
1. **건식 레지스트 ADI/AEI OPC 모델 정량 평가**: ADI(노광 후)와 AEI(탄소 오픈 후) 두 단계에서의 OPC 모델 정확도 종합 분석
2. **물리 기반 vs. ML 기반 엔진 비교**: Tachyon FEM+(물리 기반)과 Newron(ML 기반) 두 엔진의 32nm 피치 BEOL 레이어 적용 정확도 직접 비교
3. **건식 레지스트 OPC 특성화**: MOR(Metal Oxide Resist) 건식 레지스트의 OPC 모델링 특성(감도, CD 응답 등) 체계적 분석
4. **ADI → AEI 모델 전환**: 탄소 오픈(carbon open) 후 식각 편차를 반영한 AEI OPC 모델 구축 방법론
5. **BEOL 32nm 피치 실증**: 실제 BEOL 금속 레이어 데이터로 두 OPC 모델 엔진 정확도 비교

## 검증 방법론
- ASML Tachyon 소프트웨어로 ADI OPC 모델 캘리브레이션 (FEM+, Newron 각각)
- CD-SEM 측정 기반 모델 잔차(RMSE, 3σ) 비교 (ADI 및 AEI)
- Tachyon FEM+ vs. Newron 엔진의 정확도·런타임 트레이드오프 분석
- 탄소 오픈 전후 CD 변화(AEI-ADI bias)와 OPC 모델 예측의 상관관계 검증

## OPC 툴 구현 관련성
- SKOPC의 EUV 건식 레지스트 OPC 모델 구축 시 두 가지 접근법(물리 기반 vs. ML 기반) 비교 기준 제공
- `2024_Xu_OPC_model_dry_resist_lowk1_EUV_N5.md`와 함께 2024년 건식 레지스트 EUV OPC 모델 쌍두 논문
- Newron ML 엔진 기반 OPC 모델과 `2022_OPC_accuracy_deep_learning_etch_model_SPIE.md`의 etch 모델을 통합하는 SKOPC 아키텍처 설계에 참조
- SKOPC 모델 캘리브레이션 모듈에서 물리 기반/ML 기반 모델 선택 인터페이스 설계의 기반

## 태그
`Verification`, `SPIE`, `EUV`, `OPC Model`, `Dry Resist`, `MOR`, `BEOL`, `Tachyon`, `Newron`, `FEM+`, `Machine Learning`, `32nm`
