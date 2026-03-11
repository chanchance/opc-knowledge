# Direct Print EUV Patterning of Tight Pitch Metal Layers for Intel 18A Process Technology Node

## 메타데이터
- **저자**: Intel (저자 정보)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950D (2023)
- **DOI/URL**: https://doi.org/10.1117/12.2657778

## 핵심 요약
Intel 18A 공정 기술 노드의 타이트 피치 메탈 레이어 직접 인쇄 EUV 패터닝을 다룬다. 약 30-36nm 피치의 메탈 레이어에서 EUV 단일 노출(direct print) 패터닝 기술을 적용하여 이중 패터닝 없이 성능과 수율을 달성하는 방법론과 OPC 전략을 제시한다.

## 주요 기여
1. **Intel 18A EUV 직접 인쇄**: 30-36nm 피치 메탈 레이어의 EUV 단일 노출 패터닝 실증
2. **타이트 피치 OPC**: 30-36nm 피치에서의 OPC 보정 전략
3. **설계 규칙 연계**: EUV 직접 인쇄를 위한 Intel 18A 설계 규칙 최적화
4. **수율 달성**: 타이트 피치 EUV 직접 인쇄에서 생산 가능한 수율 확보

## 알고리즘/수식
### Intel 18A EUV 직접 인쇄 전략
```
Intel 18A 공정 파라미터:
  메탈 피치: ~30-36nm
  NA: 0.33 EUV
  k1 = pitch × NA / λ = 30nm × 0.33 / 13.5nm ≈ 0.73
  (단, CD는 더 작아 실질 k1 훨씬 낮음)

직접 인쇄 vs 이중 패터닝:
  이중 패터닝: 비용/복잡도 증가
  EUV 직접 인쇄: 단일 마스크 → 비용/오버레이 유리
  조건: 충분한 NILS + 공정 창 + 확률론적 수율

OPC 전략:
  확률론적 인식 OPC:
    P_fail 기반 엣지 바이어스 조정
    SRAF 최적화로 NILS 향상
  스티칭: Intel 18A는 0.33NA → 스티칭 불필요
```

### 타이트 피치 OPC 성능
```
30-36nm 피치 OPC:
  EPE_3σ < 목표값
  LCDU_3σ < 수율 요구사항
  LWR_3σ < 허용 범위

수율 분석:
  전기 저항 측정으로 수율 검증
  확률론적 결함 밀도 측정
  → EUV 직접 인쇄 수율 가능성 실증
```

## OPC 툴 SMO 구현 관련성
- Intel 18A OPC 참고: SKOPC의 30-36nm 피치 EUV OPC 성능 벤치마크
- 직접 인쇄 SMO: 타이트 피치 단일 노출을 위한 소스-마스크 최적화
- 확률론적 OPC: P_fail 기반 Intel 18A EUV 수율 최적화 OPC
- 생산 적용: 실제 Intel 파운드리 노드에서의 EUV OPC 적용 사례

## 태그
`EUV`, `Intel_18A`, `direct_print`, `tight_pitch`, `metal`, `OPC`, `single_exposure`, `yield`, `stochastic`, `SPIE`, `2023`
