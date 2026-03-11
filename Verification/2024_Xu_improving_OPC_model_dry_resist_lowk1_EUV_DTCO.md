# Improving OPC Model Accuracy of Dry Resist for Low k1 EUV Patterning

## 메타데이터
- **저자**: Dongbo Xu, Werner Gillijns, Stewart Wu, Shruti Jambaldinni, Benjamin Kam, Anuja De Silva, Germain Fenger
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540L
- **DOI/URL**: https://doi.org/10.1117/12.3010127
- **소속**: imec, Siemens EDA, Lam Research

## 핵심 요약
Low k1 EUV 패터닝을 위한 드라이 레지스트(dry resist, Lam Research EUV 건식 레지스트 시스템)의 OPC 모델 정확도를 향상시키는 방법론을 연구한다. N5 M2 설계(피치 32nm)에서 Calibre CM1 OPC 모델 정확도를 조사하고, 건식 현상(dry develop) 방식이 기존 습식 현상 대비 패턴 붕괴 감소 및 높은 도즈 감도를 제공하는 특성을 OPC 모델에 반영하는 방법을 제시한다.

## 주요 기여
1. **Calibre CM1 OPC 모델의 드라이 레지스트 적용**: N5 M2 피치 32nm에서 정확도 평가
2. 건식 현상 공정의 독특한 레지스트 특성(패턴 붕괴 없음, 높은 도즈 감도)을 OPC 모델에 반영
3. 습식 vs 건식 현상 OPC 모델 정확도 비교 분석
4. Low k1 EUV 패터닝에서 드라이 레지스트 OPC 모델의 한계 및 개선 방향 제시
5. imec-Siemens EDA-Lam Research 산학협력 기반 OPC 모델 검증 사례

## 검증 방법론
- **기술 노드**: N5 M2 설계 (피치 32nm)
- **OPC 모델**: Calibre CM1 (Siemens EDA)
- **레지스트 시스템**: Lam Research EUV 건식 레지스트 + 건식 현상
- **비교 기준**: 기존 습식 현상 레지스트 OPC 모델 정확도
- **측정 항목**: CD 예측 오차, EPE 분포, 공정 윈도우
- **환경**: imec EUV 노광 실험 환경

## OPC 툴 구현 관련성
- Calibre CM1 모델 구조에서 드라이 레지스트 파라미터 적합화 방법론
- 건식 현상 공정의 물리적 특성(수직 프로파일, 붕괴 없음)을 컴팩트 OPC 모델로 표현하는 방법
- 2025년 동일 저자 0.55NA 확장 연구(`2025_Xu_OPC_model_dry_resist_055NA_EUV_lowN_brightfield.md`)의 기반 연구
- Low k1 EUV 드라이 레지스트 OPC 모델의 현황 및 한계를 이해하는 핵심 참조

## 태그
`Verification`, `EUV`, `DryResist`, `LowK1`, `OPCModel`, `CalibeCM1`, `N5`, `DTCO`, `Lam`, `imec`, `SPIE`, `2024`
