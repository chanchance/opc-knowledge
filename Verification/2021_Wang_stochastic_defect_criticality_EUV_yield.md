# Stochastic Defect Criticality Prediction Enabled by Physical Stochastic Modeling and Massive Metrology

## 메타데이터
- **저자**: ChangAn Wang, Peigen Cao, Maxence Delorme, Jen-Yi Wuu, Jiyou Fu, Fuming Wang, Bob Lin, Yiqiong Zhao, Yi-Hsing Peng, Yongfa Fan, Mu Feng, Bin Cheng, Jen-Shiang Wang, Mark Simmoms, Stefan Hunsche, Oliver Patterson, Kuo-Feng Pao, Abdalmohsen Elmalk, Kevin Gao, Ruochong Fei, Xuefeng Zeng, Xiaolong Zhang
- **연도**: 2021
- **게재지**: Proc. SPIE 11609, Extreme Ultraviolet (EUV) Lithography XII, 1160916
- **DOI/URL**: https://doi.org/10.1117/12.2584767

## 핵심 요약
EUV 리소그래피 양산에서 스토캐스틱 효과로 인한 결함이 주요 수율 킬러(yield killer)가 된 상황에서, 물리 기반 스토캐스틱 모델링과 대용량 계측(massive metrology)을 결합하여 칩 설계 단계에서 스토캐스틱 결함 임계 hotspot을 예측하는 플로우를 제시한 논문. SEPE(Stochastic Edge Placement Error) 모델 캘리브레이션, 패턴 인식, 결함 확률 기반 hotspot 랭킹을 통합한 EUV 스토캐스틱 검증 파이프라인을 구현하였다.

## 주요 기여
1. **SEPE(Stochastic EPE) 모델 캘리브레이션 플로우**: 대용량 계측 데이터를 활용한 스토캐스틱 EPE 물리 모델 캘리브레이션 방법론
2. **결함 확률 기반 hotspot 랭킹**: 각 패턴의 결함 발생 확률을 계산하고 이를 기준으로 hotspot 위험도를 순위화
3. **패턴 인식 통합**: 설계 내 잠재적 스토캐스틱 취약 패턴을 자동으로 인식하는 알고리즘
4. **대규모 칩 설계 적용**: 소규모 테스트셀을 넘어 실제 칩 설계 전체에 스토캐스틱 hotspot 예측 적용
5. **OPC 검증 루프 통합**: 스토캐스틱 결함 예측을 OPC 보정 후 검증 단계에 통합하는 end-to-end 플로우

## 검증 방법론
- 대용량 SEM 계측 데이터(massive metrology)로 SEPE 모델 파라미터 캘리브레이션
- 모델 예측 결함 확률 대 실제 웨이퍼 결함 발생률 비교 검증
- 결함 확률 랭킹 기반 hotspot 포착률(recall) 및 false alarm 분석
- OPC 보정 전후 스토캐스틱 hotspot 수 변화 정량 비교

## OPC 툴 구현 관련성
- SKOPC EUV 스토캐스틱 OPC 검증 모듈의 hotspot 랭킹 알고리즘 설계 시 핵심 참조
- `2021_Latypov_Gaussian_random_field_EUV_stochastic_metrics.md`의 GRF 이론을 실제 칩 설계에 적용하는 후속 실용화 논문
- `2024_Wang_stochastic_OPC_cost_function_EUV.md`(기수집)와 함께 EUV 스토캐스틱 OPC 검증 계보 구성
- SKOPC의 PWO(Process Window Optimizer) 모듈에서 스토캐스틱 결함률을 최적화 지표로 통합 시 참조

## 태그
`Verification`, `SPIE`, `EUV`, `Stochastic`, `SEPE`, `Defect`, `Yield`, `Hotspot`, `OPC`, `Massive Metrology`
