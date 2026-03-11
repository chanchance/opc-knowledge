# Extreme UV Self-Aligned Double Patterning Process Optimization for BEOL Interconnections on 3nm Nodes and Beyond

## 메타데이터
- **저자**: Montero et al.
- **연도**: 2024
- **게재지**: Proc. SPIE 12958, Advanced Etch Technology and Process Integration for Nanopatterning XIII, 129580D (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010454

## 핵심 요약
3nm 노드 이하 BEOL(Back-End-Of-Line) 인터커넥트 배선을 위한 EUV 자기 정렬 이중 패터닝(SADP) 공정 최적화를 제시한다. EUV SADP는 단일 EUV 노출로 달성하기 어려운 미세 피치 금속 배선을 구현하는 핵심 기술로, 공정 최적화를 통해 CD 균일성과 오버레이 성능을 향상시킨다.

## 주요 기여
1. **EUV SADP BEOL 최적화**: 3nm 이하 노드 금속 배선용 EUV SADP 공정 최적화
2. **CD 균일성 향상**: SADP 공정에서 스페이서 기반 CD 제어 최적화
3. **오버레이 제어**: EUV SADP에서 자기 정렬 특성을 활용한 오버레이 향상
4. **BEOL 확장성**: SADP로 단일 패터닝 한계 이하 피치 실현

## 알고리즘/수식
### EUV SADP 공정 플로우
```
EUV SADP 단계:
  1. EUV 노출: Mandrel 패턴 정의 (pitch_final = 2 × pitch_EUV)
  2. Trim 에칭: Mandrel CD 조정
  3. 스페이서 증착: 균일한 두께 t_spacer 증착
  4. Spacer 에칭: 이방성 에칭으로 스페이서만 남김
  5. Mandrel 제거: 최종 스페이서 패턴 = pitch_final

CD 제어:
  CD_spacer = t_spacer (스페이서 두께에 의존)
  CD_uniformity ∝ t_spacer_uniformity

피치 분할:
  pitch_EUV → pitch_final = pitch_EUV / 2
  → EUV 해상도 한계 극복
```

### SMO/OPC Mandrel 최적화
```
Mandrel OPC 목표:
  - Mandrel CD 균일성 최대화
  - Mandrel 엣지 거칠기 최소화 (LWR → 스페이서 LWR로 전달)

Mandrel SMO:
  최적 소스 형상: Mandrel 패턴의 NILS/EL 최대화
  → 스페이서 CD 균일성 향상에 기여
```

## OPC 툴 SMO 구현 관련성
- SADP Mandrel OPC: SKOPC에서 SADP Mandrel 레이어 OPC 지원
- Mandrel SMO: Mandrel 패턴에 최적화된 소스 형상 도출
- BEOL 금속 배선: 3nm 이하 노드 BEOL 레이어 OPC/SMO 방향
- 피치 분할 전략: SADP 공정을 고려한 OPC 플로우 설계

## 태그
`EUV`, `SADP`, `double_patterning`, `BEOL`, `3nm`, `interconnect`, `spacer`, `mandrel`, `CD_uniformity`, `OPC`, `SMO`, `SPIE`
