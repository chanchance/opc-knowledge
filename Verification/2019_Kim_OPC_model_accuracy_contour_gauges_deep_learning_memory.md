# OPC Model Accuracy Study Using High Volume Contour Based Gauges and Deep Learning on Memory Device

## 메타데이터
- **저자**: Young-Seok Kim, SeIl Lee, Zhenyu Hou, Yiqiong Zhao, Meng Liu, Yunan Zheng, Qian Zhao, Daekwon Kang, Lei Wang, Mark Simmons, Mu Feng, Jun Lang, Byoung-Il Choi, Gilbert Kim, Hakyong Sim, Jongcheon Park, Gyun Yoo, JeonKyu Lee, Sung-woo Ko, Jaeseung Choi, Cheolkyun Kim, Chanha Park
- **연도**: 2019
- **게재지**: Proc. SPIE 10959, Metrology, Inspection, and Process Control for Microlithography XXXIII, 1095913 (2019년 3월 26일)
- **DOI/URL**: https://doi.org/10.1117/12.2515274

## 핵심 요약
메모리 디바이스 제조에서 OPC 모델 정확도를 향상시키기 위해 대량(>10K)의 컨투어 기반 엣지 배치 게이지(EPG)와 딥러닝을 결합한 방법을 제안한다. eBeam 툴을 이용한 빠른 컨투어 추출로 TAT(Turnaround Time) 증가 없이 OPC 모델 정확도를 >47% 개선하였다.

## 주요 기여
1. **고밀도 컨투어 기반 게이지**: fast eBeam 툴과 계측 소프트웨어로 10K 이상의 컨투어 기반 EPG 생성 (기존 CD 기반 대비 대폭 증가)
2. **딥러닝 기반 OPC 모델**: 물리 안내(physical guidance) 모델로 정규화된 딥 신경망을 OPC 모델 정확도 향상에 적용
3. **>47% 정확도 향상**: 1,400개 이상의 검증 게이지에서 기존 방법 대비 47% 이상의 모델 정확도 향상 입증
4. **오버피팅 방지**: 물리 기반 가이던스 모델로 딥러닝의 오버피팅 문제 해결

## 검증 방법론
- 10K 이상의 컨투어 기반 EPG로 모델 캘리브레이션 후 1,400개 이상의 독립 검증 게이지 평가
- 기존 CD 기반 방법과 컨투어 기반 딥러닝 방법의 모델 RMS 오차 비교
- 물리 가이던스 모델 유무에 따른 딥러닝 정확도 및 일반화 성능 비교

## OPC 툴 구현 관련성
- `skopc/modeling/` 내 OPC 모델 캘리브레이션 모듈에 컨투어 기반 고밀도 게이지 처리 기능 통합 가능
- GNN-OPC 등 신경망 기반 OPC 모델에 물리 제약 정규화 기법 적용 시 참고
- 메모리 디바이스 OPC에서 대규모 컨투어 데이터를 효율적으로 처리하는 파이프라인 설계 참고
- 딥러닝 OPC 모델의 오버피팅 방지 전략으로 활용

## 태그
`Verification`, `SPIE`, `OPC_Model`, `Contour`, `Deep_Learning`, `EPG`, `Memory_Device`, `Accuracy`, `2019`
