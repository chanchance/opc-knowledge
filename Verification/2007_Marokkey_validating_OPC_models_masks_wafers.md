# Validating Optical Proximity Correction with Models, Masks, and Wafers

## 메타데이터
- **저자**: Sajan Marokkey, Edward W. Conrad, Emily E. Gallagher, Hidehiro Ikeda, James A. Bruce, Mark Lawliss
- **연도**: 2007
- **게재지**: Proc. SPIE 6730, Photomask Technology 2007, 67302Q
- **DOI/URL**: https://doi.org/10.1117/12.746685

## 핵심 요약
OPC 모델, 마스크, 웨이퍼 세 가지 차원에서 OPC 결과를 통합 검증하는 종합적 OPC 검증 방법론을 제시한 논문. 입력 설계 형상에서 마스크 데이터, 최종 웨이퍼 이미지까지 각 단계에서 크게 달라지는 OPC 보정 결과를 모델 기반 검증 프로그램으로 체계적으로 검증하는 프레임워크를 구축하고, 선택적 형상 바이어싱, 패턴 특정 보정, 다중 노광 조건 모델링 효과를 포함하여 검증하였다.

## 주요 기여
1. **3단계 통합 OPC 검증 프레임워크**: 모델(시뮬레이션), 마스크(실제 제조), 웨이퍼(실측) 세 차원에서의 통합 검증 방법론
2. **선택적 형상 바이어싱 검증**: OPC가 적용한 선택적 CD 바이어싱의 정확도를 각 단계에서 추적 검증
3. **다중 노광 조건 검증**: 단일 노광 조건뿐 아니라 포커스-도즈 변동을 포함한 다중 공정 조건에서의 OPC 검증
4. **OPC 검증 프로그램 호출 체계**: OPC 검증 프로그램을 체계적으로 호출하고 결과를 통합 분석하는 워크플로우
5. **마스크-웨이퍼 OPC 결과 일관성 분석**: 마스크 측정 결과와 웨이퍼 CD 측정 결과 간의 OPC 예측 일관성 평가

## 검증 방법론
- OPC 시뮬레이션 결과와 실제 마스크 CD 측정 비교 (모델-마스크 검증)
- 마스크 CD 측정 결과와 웨이퍼 CD 측정 비교 (마스크-웨이퍼 검증)
- OPC 시뮬레이션과 실제 웨이퍼 측정 직접 비교 (종단간 검증)
- 다중 포커스-도즈 조건에서의 EPE 분포 비교

## OPC 툴 구현 관련성
- SKOPC의 OPC 검증 모듈 설계에서 모델-마스크-웨이퍼 3단계 검증 체계의 기초 문헌
- OPC 검증 리포트 항목(모델 잔차, 마스크 오차, 웨이퍼 EPE)의 표준 구성 근거
- `2016_Hamouda_combining_mask_OPC_verification_yield.md`의 결합 검증 개념의 초기 선행 연구
- SKOPC Verification 모듈에서 "simulation-only", "mask+simulation", "full wafer" 검증 모드를 분리 구현할 때 참조

## 태그
`Verification`, `SPIE`, `OPC`, `Model`, `Mask`, `Wafer`, `EPE`, `Process Window`, `CD`, `Photomask Technology`
