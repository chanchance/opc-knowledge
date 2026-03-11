# Aerial Image Metrology (AIMS) Based Mask-Model Accuracy Improvement for Computational Lithography

## 메타데이터
- **저자**: (ZEISS / SPIE Photomask Technology 2022 발표)
- **연도**: 2022
- **게재지**: Proc. SPIE 12293, Photomask Technology 2022
- **DOI/URL**: https://doi.org/10.1117/12.2641724

## 핵심 요약
ZEISS AIMS EUV 장비를 이용한 직접 공중 이미지 측정으로 마스크 효과를 정량화하고, OPC 모델 교정 정확도를 향상시키는 방법을 연구한다. AIMS 기반 마스크 모델 교정, 패턴 시프트 검출, 광학 공정 윈도우 특성화에 활용한다.

## 주요 기여
1. ZEISS AIMS EUV 도구를 활용한 직접 공중 이미지 측정 기법
2. 마스크 효과(OPC, SRAF, 3D 마스크 효과) 정량화 방법론
3. AIMS 데이터를 OPC 모델 교정에 직접 통합하는 흐름 개발
4. 패턴 시프트 검출 및 마스크 자격 검증(mask qualification) 응용
5. 광학 공정 윈도우(OPW) 특성화에서 AIMS의 유용성 입증

## 모델 수식/아키텍처
- AIMS 측정 데이터: 직접 공중 이미지 강도 분포 I(x,y)
- 마스크 모델 교정: SEM CD 데이터와 AIMS 공중 이미지 데이터의 결합 교정
- 마스크 모델 잔차: ΔCD = CD_simulated - CD_AIMS_calibrated
- EPE 예산 분석: AIMS 기반 마스크 기여분 분리 정량화

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 모델 교정 시 SEM CD 외 AIMS 데이터 활용 경로 제시
- 마스크 제조 오차(CDU, placement error)가 OPC 모델에 미치는 영향 분리
- SKOPC 모델 교정 파이프라인의 마스크 모델 정확도 개선 참조
- EUV 마스크 자격 검증 및 OPC 검증(verification) 흐름에 통합 가능

## 태그
`Model`, `Optical`, `AIMS`, `MaskModel`, `EUV`, `Calibration`, `Metrology`, `SPIE`, `Photomask`
