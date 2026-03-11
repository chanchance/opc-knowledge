# Patterning Optimization for Single Exposure BLP and SNLP DRAM Layers with 0.33NA and 0.55NA EUV Lithography

## 메타데이터
- **저자**: (SPIE 13428 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13428, Advanced Etch Technology and Process Integration for Nanopatterning XIV, 1342807 (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3052xxx (SPIE 13428, 2025)

## 핵심 요약
0.33NA 및 0.55NA EUV 리소그래피에서 DRAM의 BLP(Bit-Line Periphery)와 SNLP(Storage-Node Landing Pad) 레이어의 단일 노출 패터닝 최적화를 다룬다. 두 레이어 모두 2D 패턴 복잡도가 높아 EUV SMO/OPC 최적화가 필수적이며, 0.33NA에서 0.55NA로의 전환에 따른 패터닝 성능 개선을 분석한다.

## 주요 기여
1. **BLP 단일 노출 최적화**: 비트라인 주변부 레이어의 0.33NA/0.55NA EUV 단일 마스크 패터닝 최적화
2. **SNLP 단일 노출 최적화**: 스토리지 노드 착지패드의 EUV 단일 노출 공정 창 확보
3. **NA 전환 효과 분석**: 0.33NA에서 0.55NA 전환 시 DRAM 패터닝 성능 개선 정량화
4. **SMO/OPC 전략**: BLP/SNLP 2D 패턴을 위한 소스-마스크 최적화 전략 제시

## 알고리즘/수식
### BLP/SNLP EUV 패터닝 최적화
```
DRAM EUV 패터닝 핵심 레이어:
  BLP (Bit-Line Periphery):
    - 비트라인 주변부 2D 복잡 패턴
    - 연결부(junction) 피처 + 라인/스페이스 혼합
    - 단일 EUV 노출 필요 (이중 패터닝 대체)

  SNLP (Storage-Node Landing Pad):
    - 스토리지 노드 착지패드 어레이
    - 주기적 + 비주기적 패턴 혼재
    - CD 균일성 및 오버레이 정확도 요구

NA별 패터닝 특성:
  0.33NA EUV:
    HP ≥ 16nm (반피치 한계)
    DOF ~100nm, 공정 창 제한적
  0.55NA EUV:
    HP ≥ 10nm (아나모픽)
    DOF 감소하나 해상도 대폭 향상

SMO 최적화 목표:
  max_{J, M} EPE_budget
  subject to: EL > 5%, DOF > 80nm, MEF < 3
```

### BLP/SNLP 공정 창 최적화
```
BLP 공정 창:
  PW_BLP = ∩_{피처 타입} PW_feature_i
  피처 타입: 라인끝, 코너, 밀집/고립 전환부

SNLP 공정 창:
  PW_SNLP = min(PW_array, PW_periphery)
  어레이 피치 vs 주변부 피처 동시 최적화

0.55NA 이점:
  더 강한 광학적 콘트라스트 → NILS 향상
  → BLP/SNLP 공정 창 확대
  단, 아나모픽 배율(4x/8x)로 스티칭 필요
```

## OPC 툴 SMO 구현 관련성
- DRAM BLP/SNLP SMO: SKOPC SMO에서 DRAM 특화 2D 레이어 최적화 지원
- NA별 최적화 분기: 0.33NA/0.55NA 두 광학 설정에서 동일 레이아웃 SMO
- 공정 창 최대화: EL×DOF 곱 최대화하는 소스-마스크 동시 최적화
- 스티칭 인식: 0.55NA에서 BLP/SNLP 스티칭 경계 OPC 연속성

## 태그
`DRAM`, `BLP`, `SNLP`, `EUV`, `0.33NA`, `0.55NA`, `single_exposure`, `patterning`, `SMO`, `OPC`, `process_window`, `SPIE`, `2025`
