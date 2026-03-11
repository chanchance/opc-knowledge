# Advancing EUV Patterning Through Pattern Shaping at Intel 18A Process Technology Node

## 메타데이터
- **저자**: Robert Browning, Shurong Liang, Peter Sun, Laxmy Menon, Nadjoua Moumen, Can Guven, Nathan Strutt, Mehmet Aykol, Robert Bigwood, Sarah Williams, Kevin Anglin, Amol Gupta, Steven Sherman, Kevin Fischer, Charles Wallace, Gang Shu, Bhavin Shah, Brad Taylor
- **연도**: 2024
- **게재지**: Proc. SPIE PC12958, Advanced Etch Technology and Process Integration for Nanopatterning XIII, 0000
- **DOI/URL**: https://doi.org/10.1117/12.3010982

## 핵심 요약
Intel 18A 공정 기술 노드에서 EUV stochastic 노이즈 문제를 해결하기 위한 패턴 쉐이핑(pattern shaping) 기법을 적용하여 패터닝 전략을 고도화한다. 패턴 쉐이핑을 공정 플로우에 통합함으로써 추가 EUV 패터닝 레이어 불필요, 공정 복잡성 감소, 웨이퍼 수율 향상을 동시에 달성한다. OPC와 결합된 패턴 쉐이핑으로 Intel 18A EUV 패터닝의 한계를 확장한다.

## 주요 기여
1. **Intel 18A 패턴 쉐이핑 통합**: EUV stochastic 노이즈 완화를 위한 패턴 쉐이핑 공정 통합
2. **추가 EUV 레이어 불필요**: 패턴 쉐이핑으로 복잡한 추가 노광 대체 → 공정 단순화
3. **웨이퍼 수율 향상**: stochastic 결함 감소 → 수율 개선
4. **OPC-패턴쉐이핑 공동 최적화**: OPC와 패턴 쉐이핑의 통합 최적화 전략
5. **Intel 18A RibbonFET 적용**: 차세대 GAA 트랜지스터 공정에서 EUV 패터닝 고도화

## Recipe/Flow 상세
- **패턴 쉐이핑 + OPC 통합 플로우**:
  1. **패턴 쉐이핑(Pattern Shaping) 개념**:
     - 이온 빔(directional ion beam) 또는 플라즈마 처리로 레지스트/하드마스크 형상 수정
     - stochastic 노이즈 완화: 거친 에지를 물리적으로 평탄화
     - Applied Materials Sculpta 또는 TEL Acrevia 장비 활용
  2. **EUV OPC 설계 수정**:
     - 패턴 쉐이핑 효과를 고려한 OPC 타겟 설정
     - 쉐이핑 후 형상 예측 모델을 OPC 루프에 통합
     - 쉐이핑-OPC 공동 최적화
  3. **공정 플로우 통합**:
     - EUV 노광 → 현상 → 패턴 쉐이핑 → 에치 순서
     - 쉐이핑 파라미터(방향, 에너지, 시간) 최적화
     - 쉐이핑 후 CD 및 형상 품질 측정
  4. **stochastic 개선 검증**:
     - LER/LWR 개선 측정
     - 브리지(bridge) 및 단선(break) 결함률 감소 확인
     - 쉐이핑 전후 핫스팟 분포 비교
  5. **양산 적용**:
     - Intel 18A RibbonFET 공정 레이어에 통합
     - 패턴 쉐이핑 추가로 다른 복잡한 공정 단계 제거
     - 전체 공정 BOM(Bill of Materials) 단순화
- **패턴 쉐이핑 장점**:
  - stochastic 결함 감소: 물리적 에지 평탄화로 LWR 개선
  - tip-to-tip 간격 확보: 쉐이핑으로 패턴 끝부분 형상 개선
  - 추가 EUV 레이어 대체: 비용 및 공정 복잡성 절감
- **Intel 18A 특성**: RibbonFET(GAA), PowerVia(후면 전력), EUV 직접 패터닝

## OPC 툴 구현 관련성
- SKOPC 패턴 쉐이핑 효과를 OPC 시뮬레이션 모델에 통합
- `pattern_shaping_model.py`: 이온 빔 쉐이핑 후 형상 변화 예측 모델
- OPC 타겟 설정 시 패턴 쉐이핑 예상 효과 사전 보상
- Intel 18A급 EUV 패터닝의 stochastic 개선 전략 참고

## 태그
`EUV`, `PatternShaping`, `Intel18A`, `Stochastic`, `OPC`, `RibbonFET`, `LWR`, `Manufacturing`, `Yield`, `SPIE`, `2024`
