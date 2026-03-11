# EUV OPC Modeling of Dry Photoresist System for Pitch 32nm BEOL

## 메타데이터
- **저자**: Jyun-Ming Chen, David Rio, Maxence Delorme et al. (Lam Research)
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530C
- **DOI/URL**: https://doi.org/10.1117/12.3010402

## 핵심 요약
Lam Research의 EUV 드라이 레지스트(dry develop 기술)를 피치 32nm BEOL 레이어에 적용한 OPC 모델링을 연구한다. 드라이 레지스트는 패턴 붕괴(pattern collapse)에 강하고 기존 레지스트 대비 높은 감도를 가지며, OPC 모델 정확도를 종합적으로 정량화·특성화한다.

## 주요 기여
1. Lam EUV 드라이 레지스트(건식 현상) 공정 특성화 및 OPC 모델 구축
2. 피치 32nm BEOL 레이어에서 OPC 모델 정확도 종합 평가
3. 드라이 레지스트의 고감도(high dose sensitivity)와 패턴 붕괴 저항성 분석
4. 습식 현상 레지스트 대비 드라이 레지스트 OPC 모델 거동 차이 비교
5. 드라이 레지스트 기반 EUV OPC 흐름의 산업 적용 가능성 시연

## 모델 수식/아키텍처
- **드라이 레지스트 OPC 모델**: 금속 산화물 흡수체 기반 화학 증폭 레지스트 모델링
- 핵심 파라미터:
  - 건식 현상(dry develop) 속도 함수: R_dry = f(acid_conc, T, t_develop)
  - 낮은 산 확산 길이 σ (< 5nm) 반영
  - 높은 흡수율로 인한 비선형 공중 이미지-레지스트 응답 보정
- OPC 교정: 피치/CD 스캔 기반 1D + 2D 패턴 혼합 게이지
- EUV 광학 모델: 마스크 3D 효과 및 입사각 의존성 포함

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC에 드라이 레지스트 모델 지원 추가 시 핵심 참조 논문
- Lam Research 드라이 레지스트 공정의 OPC 모델 파라미터 범위 이해
- High-NA EUV(0.55NA) 로드맵에서 드라이 레지스트가 유력 후보
- `2024_Xu_DryResist_LowK1_EUV_OPC.md` (imec 연구)와 교차 비교 가능

## 태그
`Model`, `EUV`, `DryResist`, `BEOL`, `OPC`, `LamResearch`, `Calibration`, `Pitch32nm`, `SPIE`
