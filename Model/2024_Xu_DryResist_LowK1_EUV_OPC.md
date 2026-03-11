# Improving OPC Model Accuracy of Dry Resist for Low k1 EUV Patterning

## 메타데이터
- **저자**: Dongbo Xu, Werner Gillijns, Stewart Wu, Shruti Jambaldinni, Benjamin Kam, Anuja De Silva, Germain Fenger
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540L
- **DOI/URL**: https://doi.org/10.1117/12.3010127

## 핵심 요약
EUV 저 k1 패터닝에서 드라이 레지스트(dry resist) 공정의 OPC 모델 정확도를 개선하는 방법을 연구한다. N5 M2 디자인(피치 32nm)에서 Calibre CM1 OPC 모델 정확도를 평가하고 드라이 레지스트 특유의 거동을 모델에 통합하는 방법을 제시한다.

## 주요 기여
1. 드라이 레지스트(금속 산화물 기반 EUV 레지스트) OPC 모델 교정 방법론 제시
2. N5 M2 레이어(피치 32nm) 기준 Calibre CM1 모델 정확도 평가
3. 드라이 레지스트의 고유 특성(높은 흡수율, 낮은 확산 거리)을 모델에 반영
4. 저 k1 EUV 패터닝 조건에서 OPC 모델 정확도 한계 및 개선 방향 분석
5. 드라이 레지스트와 습식(wet) 레지스트 OPC 모델 거동 비교

## 모델 수식/아키텍처
- **CM1 레지스트 모델**: 산 확산 길이(σ), 대비 파라미터(n), 임계값(t_r) 등
- 드라이 레지스트 특성 반영: 확산 길이 σ 최소화, 비선형 공중 이미지 응답
- EUV 광학 모델: 6° 경사 입사, 마스크 그림자 효과 포함
- 저 k1 조건 (k1 < 0.3): SRAF 의존성, 공정 윈도우 축소 영향 모델링
- 교정 게이지: 1D/2D 패턴 혼합, 초점 노출 행렬(FEM) 데이터 포함

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC EUV OPC 모듈에서 드라이 레지스트 지원 추가 시 핵심 참조
- High-NA EUV(0.55NA)에서 드라이 레지스트가 주요 후보 → 조기 모델 준비 필요
- Calibre CM1 모델 구조와 드라이 레지스트 파라미터 공간 이해에 유용
- `2025_Xu_DryResist_OPCModel_0p55NA.md` (기존)와 연계하여 읽을 것

## 태그
`Model`, `EUV`, `DryResist`, `LowK1`, `OPC`, `CM1`, `Calibration`, `N5`, `SPIE`, `DTCO`
