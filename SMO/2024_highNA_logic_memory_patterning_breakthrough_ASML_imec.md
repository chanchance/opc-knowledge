# Logic and Memory Patterning Breakthrough Using High-NA Lithography

## 메타데이터
- **저자**: (ASML/imec 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 13216, Photomask Technology + EUV Lithography 2024, 1321604 (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3047176

## 핵심 요약
ASML TWINSCAN EXE:5000 고NA EUV 스캐너를 사용하여 로직 및 메모리 피처의 초기 패터닝 결과를 제시한다. A14 및 A10 노드용 랜덤 로직 메탈/비아 구조, 양방향(bidirectional) 설계, 메모리 응용 결과를 포함하며, 고NA EUV가 공정 복잡성 감소, 수율 향상, 고해상도를 통해 Moore의 법칙을 계속 가능하게 함을 실증한다.

## 주요 기여
1. **고NA EUV 초기 실증 결과**: TWINSCAN EXE:5000으로 A14/A10 노드 패터닝 달성
2. **로직/메모리 통합 평가**: 랜덤 로직 메탈, 비아, 메모리 레이어 결과 제시
3. **양방향 설계 가능성**: 고NA EUV로 이전에 불가능했던 양방향 패턴 실현
4. **공정 복잡성 감소**: 다중 패터닝 불필요 → 수율 및 처리량 향상

## 알고리즘/수식
### 고NA EUV 패터닝 성능 (TWINSCAN EXE:5000)
```
고NA EUV 사양:
  NA: 0.55 (0.33NA 대비 67% 향상)
  k1 하한: k1_min = 0.18 (0.33NA: k1 ≈ 0.30)
  해상도: CD_min = k1 × λ / NA ≈ 0.18 × 13.5nm / 0.55 ≈ 4.4nm

A14 노드 응용:
  메탈 피치: ~24nm 이하
  비아 피치: ~24nm 이하
  양방향 메탈: 고NA로 가능

A10 노드 응용:
  메탈 피치: ~20nm 이하
  고NA 단일 패터닝으로 구현

SMO/OPC 역할:
  고NA 소스 최적화: 새로운 NA/σ에 최적화
  M3D 강화 보정: 고NA에서 더욱 중요한 M3D OPC
```

### 성능 메트릭
```
로직 메탈/비아:
  CD_uniformity: 3σ CD 균일성
  EPE: 엣지 배치 오차
  Process Window: DOF × EL

메모리:
  LCDU: 로컬 CD 균일성 (컨택 홀)
  Stochastic fail rate: ppm 수준
```

## OPC 툴 SMO 구현 관련성
- 고NA EUV 실증 데이터: SKOPC 고NA SMO/OPC 개발의 실제 성능 기준
- A14/A10 노드 SMO: 최소 피치 20~24nm에서 SMO 최적화 목표
- 양방향 설계 SMO: 수평/수직 혼합 패턴에 최적화된 소스 형상
- TWINSCAN EXE:5000 지원: 고NA EUV 스캐너 광학 파라미터 기반 SMO/OPC 모델

## 태그
`EUV`, `high_NA`, `0p55NA`, `logic`, `memory`, `A14`, `A10`, `ASML`, `imec`, `TWINSCAN`, `patterning`, `SMO`, `OPC`, `SPIE`, `2024`
