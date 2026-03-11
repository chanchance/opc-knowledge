# Improving OPC Model Accuracy of Dry Resist for Low k1 EUV Patterning

## 메타데이터
- **저자**: Dongbo Xu, Werner Gillijns, Stewart Wu, Shruti Jambaldinni, Benjamin Kam, Anuja De Silva, Germain Fenger
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540L
- **DOI/URL**: https://doi.org/10.1117/12.3010127

## 핵심 요약
0.33NA EUV 리소그래피가 양산에 적용된 이후 더 낮은 k1 패터닝을 위해 건식 레지스트(dry resist) 공정 도입이 요구되는 상황에서, N5 M2 레이어(피치 32nm) 건식 레지스트의 Calibre CM1 OPC 모델 정확도를 체계적으로 평가한 논문. 해상도, 거칠기, 결함, 공정 윈도우 요구사항을 충족하기 위한 신규 레지스트·공정 도입 시 OPC 모델 구축의 실용적 방법론을 제시하였다.

## 주요 기여
1. **건식 레지스트 Calibre CM1 OPC 모델 평가**: N5 M2 피치 32nm 건식 레지스트 공정에 특화된 CM1 OPC 모델 정확도 체계적 측정
2. **ADI vs. AEI 모델 비교**: ADI(After Develop Inspection)와 AEI(After Etch Inspection, after carbon open) OPC 모델 정확도 비교
3. **저-k1 EUV 패터닝 OPC 모델 요구사항 정의**: 건식 레지스트가 요구하는 OPC 모델 구축 요구사항 체계화
4. **신규 레지스트 OPC 도입 방법론**: 양산 플로우에 신규 레지스트·공정을 OPC와 함께 도입하는 실용적 방법론
5. **imec N5 실증**: imec N5 기술 노드 실제 데이터를 기반으로 건식 레지스트 OPC 모델 검증

## 검증 방법론
- N5 M2 32nm 피치 건식 레지스트 EUV 노광 웨이퍼의 CD-SEM 측정
- Calibre CM1 OPC 모델 캘리브레이션 및 잔차(RMSE, max EPE) 분석
- ADI OPC 모델과 AEI OPC 모델의 정확도 비교 (etch bias 반영 여부 영향)
- 기존 습식 레지스트 OPC 모델 파라미터 대비 건식 레지스트 모델의 차이 분석

## OPC 툴 구현 관련성
- SKOPC의 EUV 건식 레지스트 OPC 모델 지원 기능 설계 시 핵심 참조
- `2025_Xu_OPC_model_dry_resist_055NA_EUV.md`(동일 1저자)의 선행 연구로, 0.33NA → 0.55NA 건식 레지스트 OPC 모델 발전 계보
- `2021_Xu_NXE3400_OPC_process_monitoring_model_validity.md`(동일 1저자)와 함께 Xu 연구팀의 EUV OPC 모델 시리즈 구성
- SKOPC `LithoEngine`의 건식 레지스트(MOR) 모델 파라미터 추가 시 기준 정확도 벤치마크 제공

## 태그
`Verification`, `SPIE`, `EUV`, `OPC Model`, `Dry Resist`, `MOR`, `Low-k1`, `N5`, `ADI`, `AEI`, `Calibre CM1`
