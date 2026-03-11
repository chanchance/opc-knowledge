# EUV Single Patterning of Random Logic Via Using Bright Field Mask

## 메타데이터
- **저자**: imec 연구진
- **연도**: 2023
- **게재지**: Proc. SPIE 12494, Optical and EUV Nanolithography XXXVI, 124940X
- **DOI/URL**: https://doi.org/10.1117/12.2658344

## 핵심 요약
0.33NA EUV 단일 패터닝으로 랜덤 로직 via 레이어를 구현하기 위한 Ta계 bright field 마스크 솔루션을 탐색한다. 랜덤 via 패턴에서 Ta계 bright field 마스크가 최적의 RET(Resolution Enhancement Technology) 솔루션을 제공함을 보이고, OPC 및 SMO와 결합한 bright field EUV via 단일 패터닝 실현 가능성을 실증한다.

## 주요 기여
1. **랜덤 Via Bright Field EUV 단일 패터닝**: 0.33NA EUV로 랜덤 로직 via를 bright field 마스크로 단일 노광 구현
2. **Ta계 Bright Field 마스크 우위**: 랜덤 via 패턴에서 Ta계 bright field가 최적 RET 솔루션
3. **Via 층 OPC 전략**: Bright field via 층에 최적화된 OPC 방법론
4. **Stochastic 결함 관리**: Via 단일 노광에서 EUV stochastic 결함 최소화 전략
5. **공정 창 평가**: 다양한 via 크기 및 배치 패턴에서 공정 창 측정

## Recipe/Flow 상세
- **EUV Bright Field Via 단일 패터닝 OPC 플로우**:
  1. **마스크 톤 선택**:
     - Bright field (BF): 기판이 밝음, via 홀이 어두운 패턴
     - Dark field (DF): 기판이 어두움, via 홀이 밝은 패턴
     - Via 층: BF 마스크 + NTD 레지스트 또는 DF 마스크 + 양성 톤 레지스트
  2. **마스크 흡수체 선택**:
     - Ta계 이진 마스크: 표준 EUV 마스크
     - High-k 마스크: 높은 소광계수
     - Low-n attPSM: 낮은 굴절률 위상 변이
     - 랜덤 via에서 Ta계 BF가 최적 RET
  3. **SMO(Source Mask Optimization)**:
     - Via 패턴 최적화 조명 조건 (annular, multipole)
     - Bright field via의 NILS 최대화
     - SRAF 설계 (BF via용 최적 SRAF 크기/위치)
  4. **OPC 모델 캘리브레이션**:
     - BF via 층 특화 EUV OPC 모델
     - Via 크기, 피치, 배치에 따른 근접 효과 모델
     - Stochastic 거동 포함 OPC 전략
  5. **공정 창 검증**:
     - Focus-Dose 매트릭스에서 via CD 균일도 측정
     - Via 결함률(누락 via, 브리징) 측정
     - BF vs. DF 마스크 패터닝 성능 비교
- **BF Via 패터닝 장점**:
  - BF + NTD: 트렌치/via 노출 시 더 높은 이미지 대비
  - Ta계 BF: 마스크 3D 효과 상대적으로 완화
  - 랜덤 via에서 SRAF 배치 자유도 향상
- **imec N3 동등 기술 노드 적용**

## OPC 툴 구현 관련성
- SKOPC EUV via 층 OPC에서 BF/DF 마스크 톤 선택 옵션
- BF via OPC 모델: NTD 레지스트 + BF 마스크 특화 캘리브레이션
- SRAF 삽입 전략: BF via에 최적화된 SRAF 크기/위치 룰
- Stochastic-aware OPC: via 결함률 최소화를 위한 OPC 보정

## 태그
`EUV`, `Via`, `BrightField`, `SinglePatterning`, `OPC`, `SMO`, `RandomLogic`, `NTD`, `MaskTone`, `imec`, `SPIE`, `2023`
