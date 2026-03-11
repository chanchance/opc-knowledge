# Better Prediction on Patterning Failure Mode with Hotspot Aware OPC Modeling

## 메타데이터
- **저자**: Chih-I Wei, Stewart Wu, Yunfei Deng, Gurdaman Khaira, Ir Kusnadi, Germain Fenger, Seulki Kang, Yosuke Okamoto, Kotaro Maruyama, Yuichiro Yamazaki, Sayantan Das, Sandip Halder, Werner Gillijns, Gian Lorusso
- **연도**: 2021
- **게재지**: Proc. SPIE 11611, Metrology, Inspection, and Process Control for Semiconductor Manufacturing XXXV, 1161112
- **DOI/URL**: https://doi.org/10.1117/12.2583837

## 핵심 요약
리소그래피 실패 모드(failure mode)에 민감한 OPC 모델 캘리브레이션 방법론을 제안한 논문. 대면적 전자빔 검사(Large Field of View e-beam inspection)를 통해 확보한 hotspot 데이터를 OPC 모델 캘리브레이션에 직접 활용함으로써, 기존 1D/2D CD 측정 중심의 캘리브레이션 방식보다 실패 모드 예측 정확도를 향상시켰다.

## 주요 기여
1. **Hotspot-aware OPC 모델 캘리브레이션**: 패터닝 실패 모드(bridge, break, narrowing 등)에 대한 민감도를 높인 OPC 모델 구축 방법
2. **대면적 e-beam 검사 데이터 활용**: 기존 CD-SEM 포인트 측정 대신 대면적 전자빔 검사로 수집한 실패 패턴을 캘리브레이션 셋으로 활용
3. **실패 모드 분류 체계**: 다양한 패터닝 실패 유형을 분류하고 각 모드별 OPC 모델 응답을 정량화
4. **OPC 모델 검증 메트릭 확장**: 기존 EPE/RMS 외에 실패율(failure rate) 기반 검증 지표 도입
5. **삼성/imec/ASML/Synopsys 협력 연구**로 다기관 산업 데이터 기반 검증

## 검증 방법론
- Large Field of View e-beam inspection으로 실제 웨이퍼의 hotspot 패턴 대량 수집
- 수집된 hotspot 데이터를 OPC 모델 캘리브레이션 패턴 셋에 통합
- 캘리브레이션 전후 hotspot 예측 정확도 비교(recall, precision 기반 평가)
- CD-SEM 기반 EPE 검증과 hotspot-aware 검증 결과의 상관관계 분석

## OPC 툴 구현 관련성
- SKOPC의 OPC 모델 캘리브레이션 모듈에서 hotspot 패턴을 캘리브레이션 셋으로 지정하는 기능 설계 시 참조
- 모델 캘리브레이션 평가 지표에 실패율(failure rate) 기반 지표 추가 근거
- `2021_Wei_hotspot_aware_OPC_modeling_prediction.md`(기수집)와 상보적이며, 이 논문은 SPIE Metrology 트랙에서 검증(verification) 관점에 집중
- e-beam 검사 데이터를 OPC 검증 루프에 통합하는 아키텍처 설계의 기초 문헌

## 태그
`Verification`, `SPIE`, `Hotspot`, `OPC Model`, `Calibration`, `Failure Mode`, `e-beam Inspection`, `EPE`
