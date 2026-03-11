# Advanced PnR Logic Patterning Enabled by High-NA EUV Lithography

## 메타데이터
- **저자**: Syamashree Roy, Arame Thiam, Yannick Feurprier, Joern-Holger Franke, Kaushik Sah, Zhijin Chen, Bobo Cheng, Chenwei Gong, Balakumar Baskaran, Joost Bekaert, Kathleen Nafus, Nobuyuki Fukui, Atsushi Tsuboi, Ardavan Niroomand, Werner Gillijns, Hemant Vats, Yasser Sherazi, Victor M. Blanco Carballo
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 1342410
- **DOI/URL**: https://doi.org/10.1117/12.3051054

## 핵심 요약
ASML TWINSCAN EXE:5000 High-NA EUV 스캐너를 이용하여 imec A14 및 A10 기술 노드의 랜덤 로직 메탈 단일 패터닝을 개발한다. 타이트 피치 제약과 공격적인 tip-to-tip 간격을 가진 Place-and-Route(PnR) 로직 메탈 설계에서 0.55NA EUV 단일 노광 패터닝 성능을 평가하고, 20nm 피치 메탈 라인에서 첫 전기적 수율(100% yield) 달성 결과를 포함한다.

## 주요 기여
1. **High-NA EUV PnR 로직 단일 패터닝**: 0.55NA EXE:5000으로 A14/A10 노드 랜덤 로직 메탈 단일 노광 구현
2. **20nm 피치 100% 전기 수율**: 20nm 피치 메탈 라인에서 100% 전기 수율 최초 달성
3. **A14/A10 노드 실증**: imec A14(~1.4nm 동등), A10(~1nm 동등) 기술 노드 패터닝 성능 평가
4. **OPC + SMO + High-NA 생태계**: High-NA EUV 단일 패터닝을 위한 통합 OPC/SMO/레지스트 솔루션
5. **imec-ASML-협력사 생태계 성숙**: EXE:5000 High-NA EUV 패터닝 생태계 준비도 검증

## Recipe/Flow 상세
- **High-NA EUV PnR 로직 메탈 패터닝 플로우**:
  1. **설계 타겟 설정**:
     - A14 노드: imec 로드맵 1.4nm 동등 기술 노드
     - A10 노드: imec 로드맵 1nm 동등 기술 노드
     - 최소 메탈 피치: 20nm (A14), 더 작은 피치 (A10)
     - PnR(Place and Route) 생성 랜덤 로직 레이아웃
  2. **EXE:5000 광학 설정**:
     - 0.55NA 아나모픽 렌즈 (X: 0.55NA, Y: 0.33NA)
     - 마스크 배율: X: 4×, Y: 8× 비대칭
     - High-NA 특화 조명 조건 SMO
  3. **마스크 및 OPC**:
     - EUV 마스크 흡수체 옵션 선택 (Ta계 또는 Low-n)
     - High-NA 특화 OPC 모델 캘리브레이션
     - 아나모픽 비대칭 보정 포함 OPC
     - Stochastic-aware OPC 전략 (20nm 피치)
  4. **레지스트 및 공정**:
     - 고성능 EUV 레지스트 (CAR 또는 금속산화물)
     - 또는 건식(dry) 레지스트 옵션
     - 최적 도즈, 포커스 조건
  5. **전기 수율 측정**:
     - Serpentine 및 fork-fork 메탈 구조 전기 저항 측정
     - 20nm 피치에서 100% 전기 수율 확인
     - A14/A10 노드별 공정 창 분석
- **High-NA EUV 패터닝 특수 고려사항**:
  - 아나모픽 렌즈: X/Y 방향 비대칭 → OPC에서 방향별 처리 필요
  - 8×/4× 마스크 배율 비대칭: 마스크 설계 및 OPC 좌표 변환
  - Stitching: Field 경계에서 두 노광 결합 시 OPC 공동 최적화 필요
  - 20nm 이하 피치: stochastic 효과 더욱 중요
- **imec-ASML 공동 연구**: ASML High-NA Lab at imec에서 수행

## OPC 툴 구현 관련성
- SKOPC High-NA EUV (0.55NA) 스캐너 OPC 모델 추가
- 아나모픽 비대칭 렌즈 시스템 OPC: X/Y 파라미터 분리 처리
- 8×/4× 마스크 배율 좌표 변환 로직
- A14/A10 노드 BEOL 메탈 OPC 레시피 (20nm 이하 피치) 설계 기준

## 태그
`HighNA`, `EUV`, `0.55NA`, `PnR`, `LogicMetal`, `SinglePatterning`, `A14`, `A10`, `OPC`, `imec`, `ASML`, `ElectricalYield`, `SPIE`, `2025`
