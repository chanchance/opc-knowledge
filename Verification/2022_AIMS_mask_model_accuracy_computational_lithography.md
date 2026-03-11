# Aerial Image Metrology (AIMS) Based Mask-Model Accuracy Improvement for Computational Lithography

## 메타데이터
- **저자**: (저자명 미확인 - SPIE 12293 수록)
- **연도**: 2022
- **게재지**: Proc. SPIE 12293 (Photomask Technology 2022, 2022년 12월)
- **DOI/URL**: https://doi.org/10.1117/12.2641724

## 핵심 요약
ZEISS AIMS® EUV 툴을 이용한 직접 공중상(aerial image) 측정의 실현 가능성을 연구하고, EPE 예산과 OPC 모델 정확도에 영향을 미치는 마스크 효과 정량화에 활용한다. 공중상 계측을 OPC 모델 캘리브레이션, 패턴 시프트 검출, 정량적 마스크 계측, 광학 프로세스 윈도우 특성화에 적용하는 방법을 제시한다.

## 주요 기여
1. **AIMS EUV 기반 OPC 모델 캘리브레이션**: 직접 공중상 측정 데이터를 OPC 모델 캘리브레이션에 활용하여 마스크 모델과 포토레지스트 프로세스 모델을 분리(decouple) 보정
2. **패턴 시프트 검출**: 마스크 오차로 인한 패턴 위치 이동을 공중상 계측으로 정량화
3. **마스크 계측 정량화**: 마스크 효과가 EPE 예산에 미치는 영향을 측정하는 방법론 확립
4. **프로세스 윈도우 특성화**: 공중상 기반으로 광학 프로세스 윈도우를 정량적으로 평가

## 검증 방법론
- ZEISS AIMS® EUV 공중상 측정값과 시뮬레이션 결과 비교
- OPC 모델 캘리브레이션 전후 모델 정확도(EPE 감소) 정량 평가
- 패턴 시프트 측정의 재현성 및 민감도 분석
- 마스크-모델 분리 캘리브레이션 효과 검증

## OPC 툴 구현 관련성
- OPC 모델 캘리브레이션 파이프라인에서 AIMS 계측 데이터 입력 지원 고려
- 마스크 모델과 레지스트 모델을 분리하여 보정하는 아키텍처 설계 시 참고
- EPE 예산 관리 시스템에 마스크 오차 기여분 정량화 통합 방안으로 활용
- `skopc/modeling/` 의 모델 캘리브레이션(Calibration) 모듈과 직접 연관

## 태그
`Verification`, `SPIE`, `AIMS`, `EUV`, `OPC_Model`, `Mask_Metrology`, `EPE`, `Process_Window`, `2022`
