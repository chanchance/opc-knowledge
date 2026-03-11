# New Multi-Beam Mask Data Preparation Method for EUV High Volume Data

## 메타데이터
- **저자**: Kyungsup Shin, Sunyoung Kim, Jihyeon Choi, Eokbong Kim, Sanghee Lee, Harald Hoeller-Lugmayr, Amir Moqanaki, Annette Schnettelker, Mathias Tomandl, Christof Zillner, Yohei Torigoe, Taigo Fujii, Ryunosuke Miyake, Mizuki Odaka, Issei Masumoto, Masakazu Hamaji
- **연도**: 2023
- **게재지**: Proc. SPIE 12915, Photomask Japan 2023: XXIX Symposium on Photomask and Next-Generation Lithography Mask Technology, 129150D
- **DOI/URL**: https://doi.org/10.1117/12.2683168

## 핵심 요약
다중 빔 마스크 기록기(MBMW)를 활용한 EUV 고용량 데이터 마스크 데이터 준비(MDP) 새로운 방법을 제안한다. MBMW는 원형 및 곡선형 패턴 기록을 가능하게 했지만, 설계 데이터 꼭짓점(vertex) 수 급증과 MDP TAT(Turn-Around-Time) 증가가 문제다. 효율적인 curvilinear 데이터 처리 방법으로 EUV 마스크 제조의 실용성을 향상시킨다.

## 주요 기여
1. **MBMW용 신규 EUV MDP 방법**: 다중 빔 기록기 특화 고용량 EUV 데이터 처리 방법 개발
2. **Curvilinear 데이터 효율화**: 기존 방법 대비 vertex 수 감소 및 데이터 볼륨 압축
3. **MDP TAT 단축**: 고용량 curvilinear EUV 데이터의 MDP 처리 시간 단축
4. **MBMW 기록 최적화**: 다중 빔 기록기의 노광 패턴 최적화로 정확도 향상
5. **EUV HVM 적용 가능성**: 고용량 제조 환경에서의 curvilinear MDP 실용화

## Recipe/Flow 상세
- **MBMW EUV MDP 플로우**:
  1. **OPC/ILT 출력 데이터 수신**:
     - Curvilinear OPC 또는 ILT 결과 마스크 형상 (GDS2/OASIS 또는 MULTIGON)
     - 복잡한 곡선 형상으로 인한 대용량 데이터
  2. **데이터 전처리 및 압축**:
     - 불필요한 vertex 제거: 허용 오차 내에서 폴리곤 단순화
     - 베지어 곡선 또는 스플라인으로 변환하여 데이터 볼륨 감소
     - MULTIGON 형식: 직선+곡선 혼합 표현으로 효율화
  3. **MPC (Mask Process Correction)**:
     - MBMW 특화 MPC: e-beam 근접 효과, 포그 효과 보정
     - Curvilinear 형상에 맞는 MPC 적용
     - 마스크 제조 공차 내 보정
  4. **마스크 기록 데이터 생성**:
     - MBMW 기록 형식으로 변환 (기계 형식)
     - 다중 빔 노광 패턴 최적화
     - 기록 시간 및 데이터 전송 최적화
  5. **검증**:
     - MRC(마스크 룰 체크) 확인
     - 시뮬레이션 기반 프린터빌리티 검증
     - 실제 마스크 기록 후 CD-SEM 측정
- **MBMW 장점**:
  - 기존 단일 빔 e-beam 대비 수십~수백 배 높은 처리량
  - 병렬 다중 빔으로 복잡한 curvilinear 형상 고속 기록
  - EUV curvilinear 마스크의 HVM 적용 핵심 기술
- **소속 기관**: 삼성전자 + IMS Nanofabrication (IMS) 등 국제 공동 연구

## OPC 툴 구현 관련성
- SKOPC curvilinear 마스크 출력 데이터를 MBMW 형식으로 변환하는 MDP 모듈
- `mbmw_mdp.py`: vertex 최적화, MULTIGON 변환, MBMW 기록 데이터 생성
- Curvilinear OPC → MBMW MDP 파이프라인 연결
- EUV HVM에서 curvilinear 마스크 TAT 최적화 가이드라인

## 태그
`MBMW`, `MaskDataPreparation`, `EUV`, `Curvilinear`, `MultiBeam`, `MaskWriting`, `HVM`, `DataVolume`, `Photomask`, `SPIE`, `2023`
