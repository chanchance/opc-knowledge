# OPC Accuracy Improvement Through Deep-Learning Based Etch Model

## 메타데이터
- **저자**: (Newron/Synopsys 연구팀, 상세 저자 목록은 SPIE 원문 참조)
- **연도**: 2022
- **게재지**: Proc. SPIE 12056, Optical Microlithography XXXV, 1205607
- **DOI/URL**: https://doi.org/10.1117/12.2613926

## 핵심 요약
딥러닝 기반 etch 모델을 OPC 플로우에 통합하여 OPC 정확도를 향상시킨 논문. 풀칩 웨이퍼에서 관측된 강한 로딩 효과(loading effect)를 딥러닝 Newron etch 모델로 효과적으로 포착하고, 이를 OPC 보정에 반영함으로써 기존 룰 기반 또는 단순 모델 기반 etch 보정 대비 현저한 정확도 개선을 달성하였다.

## 주요 기여
1. **딥러닝 etch 모델(Newron) 풀칩 검증**: 전체 칩 수준에서 etch 로딩 효과 포착 능력 실증
2. **강한 로딩 효과 처리**: 하부 서브레이어(sublayer) 영향에 의한 강한 패턴 밀도 의존 etch 편차를 딥러닝 모델로 캡처
3. **OPC-etch 통합 보정 플로우**: 딥러닝 etch 모델을 OPC 루프에 직접 통합하는 실용적 방법론
4. **기존 방법 대비 정확도 비교**: 룰 기반 및 기존 모델 기반 EPC(Etch Proximity Correction) 대비 개선량 정량 제시
5. **풀칩 런타임 적합성 검증**: 딥러닝 모델의 풀칩 OPC 플로우 적용 가능한 계산 효율성 확인

## 검증 방법론
- 풀칩 웨이퍼 CD-SEM 측정 데이터와 딥러닝 etch 모델 예측값 비교
- 강한 로딩 효과 영역에서의 EPE 분포 (딥러닝 모델 적용 전후 비교)
- 다양한 패턴 밀도 환경에서의 모델 일반화 성능 평가
- OPC 수렴 후 EPE RMS 및 최대값 비교 (기존 방법 vs. 딥러닝 etch 모델 통합)

## OPC 툴 구현 관련성
- SKOPC의 딥러닝 etch 모델 통합 설계 시 핵심 참조
- `2021_Hooker_ML_etch_model_OPC_ILT.md`, `2022_Shi_deep_learning_etch_model_OPC_accuracy.md`와 함께 ML etch 모델 계보를 구성하는 중요 문헌
- `2021_Meng_ML_EPE_etch_bias_IEEE.md`의 ML 방식과 비교하여 딥러닝(feature learning) 방식의 우위 영역 파악에 활용
- 패턴 밀도 의존 로딩 효과를 처리하는 etch 모델 기능 요구사항 정의에 직접 참조

## 태그
`Verification`, `SPIE`, `Etch Model`, `Deep Learning`, `OPC Accuracy`, `Loading Effect`, `EPE`, `Full Chip`
