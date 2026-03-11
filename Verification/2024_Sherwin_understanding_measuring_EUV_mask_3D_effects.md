# Understanding and Measuring EUV Mask 3D Effects

## 메타데이터
- **저자**: Stuart Sherwin, Matt Hettermann, Dave Houser, Patrick Naulleau
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII
- **DOI/URL**: https://doi.org/10.1117/12.3012400

## 핵심 요약
EUV 마스크 3D 효과(Mask 3D effects)의 이해와 측정에 관한 논문. EUV 리소그래피에서 마스크 그림자 효과(shadowing), 마스크 위상 효과 등 두꺼운 마스크 흡수체로 인한 3D 효과가 OPC 정확도와 패터닝 성능에 미치는 영향을 정량적으로 분석한다. 마스크 3D 효과 측정 방법론과 완화 전략을 제시하며, 고정밀 EUV OPC 모델 구축을 위한 기반을 제공한다.

## 주요 기여
1. EUV 마스크 두께로 인한 3D 효과(그림자, 위상, 반사율 변화)의 체계적 측정 방법론
2. 마스크 3D 효과가 웨이퍼 레벨 패턴 피델리티에 미치는 정량적 영향 평가
3. 마스크 3D 효과 완화 전략 비교 분석
4. OPC 모델에 Mask 3D 효과를 통합하기 위한 측정 데이터 제공 방법
5. 고NA EUV 리소그래피에서 마스크 3D 효과 심화 양상 분석

## 검증 방법론
- **대상**: EUV 마스크 흡수체 두께에 따른 3D 산란/그림자 효과
- **측정 방법**: 실험적 EUV 노광 + 시뮬레이션 비교
- **평가 항목**: 마스크 3D 효과로 인한 패턴 비대칭성, Best Focus Shift, 이미지 기울기 왜곡
- **플랫폼**: LBNL ALS(Advanced Light Source) EUV 계측 환경
- **완화 방법**: OPC에서 마스크 3D 인식 보정 적용 효과 검증

## OPC 툴 구현 관련성
- EUV OPC 모델에 Mask 3D(EMF) 효과를 반드시 포함해야 함을 실험으로 입증
- 고NA EUV에서 마스크 3D 효과가 더욱 심각해지므로 OPC 모델 복잡도 증가 필요
- OPC 검증 시 마스크 3D 효과 induced 패턴 비대칭성을 별도 분리 분석해야 함
- 그림자 효과 보정 알고리즘의 효과를 측정 데이터로 검증하는 절차 수립 기준

## 태그
`Verification`, `EUV`, `Mask3D`, `Shadow`, `EMF`, `PatternFidelity`, `HighNA`, `SPIE`, `2024`
