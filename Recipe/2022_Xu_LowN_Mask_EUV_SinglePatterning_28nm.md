# Investigation of Low-N Mask in 0.33NA EUV Single Patterning at Pitch 28nm Metal Design

## 메타데이터
- **저자**: Dongbo Xu, Werner Gillijns, Ling Ee Tan, Vicky Philipsen, Ryoung-han Kim
- **연도**: 2022
- **게재지**: Proc. SPIE 12051, Optical and EUV Nanolithography XXXV, 120510H
- **DOI/URL**: https://doi.org/10.1117/12.2614197

## 핵심 요약
0.33NA EUV 단일 패터닝으로 28nm 피치 메탈 레이어를 구현하기 위한 low-n 위상 변이 마스크(attPSM)의 효과를 연구한다. imec N3(파운드리 N2 동등) 랜덤 로직 M1 레이어에서 표준 Ta계 이진 마스크, 고소광계수(high-k) 마스크, low-n attPSM의 세 마스크 후보를 SMO로 비교 평가하고, low-n attPSM이 마스크 3D 효과 완화와 공정 창 향상에서 우위를 보임을 실증한다.

## 주요 기여
1. **Low-n attPSM 우위 실증**: 28nm 피치에서 low-n 위상 변이 마스크의 마스크 3D 효과 완화 효과 정량화
2. **세 가지 마스크 후보 SMO 비교**: Ta계 이진, high-k, low-n attPSM의 체계적 SMO 비교
3. **마스크 밝기/어두운 필드 영향**: 마스크 톤(dark-field vs. bright-field)과 SRAF 유무 영향 분석
4. **imec N3 랜덤 로직 M1 검증**: 실제 로직 설계 레이아웃에서 마스크 옵션별 패터닝 성능 평가
5. **stochastic 결함 완화**: low-n attPSM으로 28nm 피치에서 EUV stochastic 결함 감소

## Recipe/Flow 상세
- **Low-n attPSM EUV OPC 평가 플로우**:
  1. **마스크 후보 정의**:
     - 표준 Ta계 이진 마스크 (현재 양산 표준)
     - High-k 흡수체 마스크 (높은 소광계수 k)
     - Low-n attPSM (낮은 굴절률 n, 위상 변이 기능)
  2. **SMO(Source Mask Optimization) 수행**:
     - 각 마스크 후보에 대해 최적 조명 조건 탐색
     - imec N3 M1 랜덤 로직 레이아웃 대상
     - 최소 피치 28nm에서 공정 창 최대화
  3. **마스크 톤 및 SRAF 영향 평가**:
     - Dark-field vs. Bright-field 비교
     - SRAF 유무 조합 평가
     - 마스크 3D 효과: 각 마스크 흡수체 두께, 굴절률 영향
  4. **OPC 모델 캘리브레이션**:
     - 마스크 3D 효과 포함 EUV OPC 모델 구성
     - Low-n attPSM 특화 마스크 3D 모델 캘리브레이션
  5. **패터닝 성능 비교**:
     - NILS, DOF, EL, PVB, stochastic 실패율 비교
     - Low-n attPSM + bright-field + SRAF 조합이 최적 성능
- **Low-n attPSM 원리**:
  - 낮은 굴절률(n < 1): 마스크 흡수체의 실수부 굴절률 감소
  - 마스크 3D 효과(M3D) 감소: shadowing 오차 완화
  - 위상 변이(phase shift): 광학 이미지 대비 향상
  - 결과: 동일 조명에서 더 높은 NILS, 더 넓은 DOF
- **imec N3 노드**: 파운드리 N2 동등, 28nm 피치 M1 메탈

## OPC 툴 구현 관련성
- SKOPC EUV 마스크 모델에서 low-n attPSM 옵션 추가
- 마스크 흡수체 굴절률(n, k) 파라미터 입력으로 마스크 3D 효과 자동 보정
- 28nm 피치 EUV OPC에서 low-n attPSM 최적화 파라미터 가이드라인
- SMO 모듈에서 마스크 타입별 최적 조명 조건 데이터베이스

## 태그
`EUV`, `LowNMask`, `attPSM`, `0.33NA`, `28nm`, `OPC`, `SMO`, `MaskAbsorber`, `M3D`, `imec`, `SPIE`, `2022`
