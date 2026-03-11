# Combining Mask and OPC Process Verification for Improved Wafer Patterning and Yield

## 메타데이터
- **저자**: Ayman Hamouda, Hesham Abdelghany
- **연도**: 2016
- **게재지**: Proc. SPIE 9985, Photomask Technology 2016, 99852A
- **DOI/URL**: https://doi.org/10.1117/12.2246563

## 핵심 요약
마스크 공정(MPC)과 리소그래피 공정(OPC) 검증을 통합하여 최종 웨이퍼 패터닝 품질을 공동으로 평가하는 결합 검증(combined-verification) 방법론을 제안한 논문. OPC 보정 잔차와 MPC 보정 잔차가 중첩될 때 발생하는 숨겨진 패터닝 열화(degradation) 위험을 사전에 포착하고 보정하는 프레임워크를 제시하였다.

## 주요 기여
1. **결합 검증 방법론(Combined Verification)**: 마스크 공정과 리소그래피 공정의 검증을 통합하여 양쪽 보정 잔차의 중첩 효과를 평가하는 새로운 프레임워크
2. **숨겨진 패터닝 열화 포착**: OPC 잔차와 MPC 잔차가 동시에 나쁜 방향으로 겹칠 때 발생하는 hidden 패터닝 위험 식별
3. **OPC-MPC 상호작용 정량화**: OPC 보정 오차와 MPC 보정 오차의 상호작용이 웨이퍼 CD에 미치는 결합 영향 계산
4. **공정 위험 조기 차단**: 마스크 제조 및 OPC 플로우에서 결합 검증을 통해 테이프아웃 전 위험 패턴 조기 발견
5. **수율 개선 경로 제시**: 결합 검증으로 발견된 취약 패턴에 대한 OPC/MPC 공동 재최적화 방법

## 검증 방법론
- OPC 잔차와 MPC 잔차를 각각 측정하고 결합 시뮬레이션으로 웨이퍼 영향 계산
- 결합 검증 전후 hotspot 발견 수 및 패터닝 오차 분포 비교
- 실제 웨이퍼 CD 측정 데이터로 결합 검증 예측 모델 검증
- 결합 검증으로만 발견 가능한 위험 패턴 유형 분류 및 통계

## OPC 툴 구현 관련성
- SKOPC 검증 모듈에서 OPC 검증과 MPC 검증을 통합하는 결합 검증 기능 설계 시 핵심 참조
- `2019_Chen_mask_process_correction_optical_weak_pattern.md`, `2023_Lyons_mask_error_OPC_model_error_EUV.md`와 함께 마스크-OPC 상호작용 연구 계보 구성
- `2017_Hamouda_OPC_recipe_coverage_hotspot.md`(기수집)의 선행 연구로, 같은 저자(Hamouda)의 검증 방법론 발전 추적
- OPC 검증 리포트에 MPC 잔차 영향을 함께 표시하는 통합 보고 형식 설계 기준

## 태그
`Verification`, `SPIE`, `MPC`, `OPC`, `Combined Verification`, `Mask Error`, `Patterning Yield`, `Wafer Quality`, `Hotspot`
