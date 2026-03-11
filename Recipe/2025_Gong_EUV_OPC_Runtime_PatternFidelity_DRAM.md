# Optimizing EUV OPC Runtime and Pattern Fidelity in DRAM Manufacturing

## 메타데이터
- **저자**: Shu De Gong, Sheng Tse Chen, Chun Cheng Liao, Teng Yen Huang, Renyang Meng, Kiho Yang, Werner Gillijns, Hsin-jung Lin, Shou-yuan Ma, JenHsiang Tsai, Ling Chieh Lin, Ryan Chou, Andrew Burbine, Alex Pearson, Xima Zhang
- **연도**: 2025
- **게재지**: Proc. SPIE 13427, Novel Patterning Technologies 2025, 134270Y
- **DOI/URL**: https://doi.org/10.1117/12.3051007

## 핵심 요약
DRAM 제조에서 EUV OPC의 런타임과 패턴 충실도를 동시에 최적화하는 메모리 OPC 플로우를 제안한다. Invited 논문으로, Micron/삼성/SK하이닉스 등 DRAM 제조사와 Siemens(Calibre)/imec 협력으로 EUV 기반 DRAM 레이어 OPC의 실제 양산 적용을 위한 런타임 단축과 패턴 충실도 향상을 달성한다.

## 주요 기여
1. **DRAM 특화 EUV OPC 플로우**: 메모리 어레이의 규칙적 패턴 구조를 활용한 최적화 OPC 플로우
2. **런타임 최적화**: 메모리 OPC 고유의 반복 패턴 특성으로 full-chip OPC 런타임 대폭 단축
3. **패턴 충실도 향상**: EUV 리소그래피 조건에서 DRAM 패턴의 CD 정확도 및 형상 충실도 개선
4. **양산 적용 실증**: HVM(High-Volume Manufacturing) 환경에서 EUV OPC 플로우 검증
5. **Siemens-imec-DRAM Fab 협력**: EDA 툴, 연구소, 제조사 삼자 협력으로 실용적 OPC 솔루션 도출

## Recipe/Flow 상세
- **DRAM EUV OPC 최적화 플로우**:
  1. **DRAM 레이아웃 분석**:
     - 규칙적 어레이 패턴(Active, Bitline, Wordline, Contact) 분류
     - 반복 단위 셀(unit cell) 식별 → OPC 연산 최소화
     - 주변 회로(periphery) 영역과 어레이 영역 분리 처리
  2. **EUV OPC 모델 캘리브레이션**:
     - DRAM 특화 EUV 공정 파라미터 캘리브레이션
     - 어레이 패턴의 근접 효과 측정 및 모델 피팅
     - Focus-dose 변동에 따른 공정 창 모델 포함
  3. **런타임 최적화 전략**:
     - 반복 패턴 캐싱(caching): 동일 패턴 환경 OPC 결과 재사용
     - 어레이 주기성 활용: 단위 셀 OPC → 전체 어레이 전파
     - 병렬 처리: 독립적인 셀/블록 동시 OPC 수행
     - ML 예측: 초기 OPC 이동량 예측으로 반복 횟수 감소
  4. **패턴 충실도 최적화**:
     - 어레이-주변부 경계 패턴 특화 OPC
     - Corner/End of line 패턴 추가 보정
     - EUV 특유의 shadowing, flare 보정 강화
  5. **양산 검증**:
     - 실제 DRAM 웨이퍼에서 OPC 결과 검증
     - CD 균일도, EPE, 핫스팟 검사
     - 런타임 및 패턴 충실도 지표 최종 보고
- **DRAM OPC 특수 고려사항**:
  - 극도로 규칙적인 어레이: OPC 최적화 기회 최대
  - 주변 회로(SA, WL driver 등): 랜덤 로직과 유사한 OPC 필요
  - EUV stochastic 효과: 메모리 컨택 레이어에서 yield 영향
- **협력 기관**: Micron Technology + Siemens EDA (Calibre) + imec

## OPC 툴 구현 관련성
- SKOPC 메모리 OPC 모드에서 어레이 반복 패턴 캐싱 구현
- `dram_opc_flow.py`: DRAM 어레이/주변부 분리 OPC 레시피
- 단위 셀 OPC 결과 재사용 로직으로 런타임 단축
- EUV DRAM 레이어별 OPC 파라미터 최적화 가이드라인

## 태그
`EUV`, `DRAM`, `Memory`, `OPC`, `Runtime`, `PatternFidelity`, `Manufacturing`, `HVM`, `Calibre`, `imec`, `SPIE`, `2025`
