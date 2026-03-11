# Novel Patterning Technology to Boost EUV Performance

## 메타데이터
- **저자**: Frederic Lazzarino, Ru-Gun Liu et al.
- **연도**: 2025
- **게재지**: Proc. SPIE 13429, Advanced Etch Technology and Process Integration for Nanopatterning XIV, 1342904 (22 April 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3055315

## 핵심 요약
EUV 패터닝 성능을 향상시키는 새로운 패터닝 기술을 제시한다. EUV 단일 인쇄의 한계를 극복하기 위한 신규 공정 기술(가스 클러스터 빔 방향성 에칭 등)과 OPC/RET 최적화를 결합하여 해상도 한계 이하의 팁-투-팁(tip-to-tip) 금속 패터닝을 달성한다.

## 주요 기여
1. **EUV 성능 향상 신규 기술**: 해상도 한계 이하 패터닝을 위한 새로운 공정 기술
2. **팁-투-팁 패터닝**: 15nm 이하 T2T 금속 PnR을 0.33NA EUV 단일 인쇄로 달성
3. **가스 클러스터 빔(GCB) 에칭**: 방향성 에칭으로 T2T 간격 제어
4. **OPC/RET 통합**: 신규 에칭 기술과 계산 리소그래피 최적화 결합

## 알고리즘/수식
### 팁-투-팁 패터닝 기술
```
문제: EUV 0.33NA에서 sub-15nm T2T 직접 인쇄 불가
  해상도 한계: CD_min ≈ k1 · λ / NA ≈ 0.28 · 13.5nm / 0.33 ≈ 11.5nm

해결책: GCB 방향성 에칭
  1. EUV OPC 인쇄: T2T 간격 > 해상도 한계로 인쇄
  2. GCB 에칭: 특정 방향으로 선택적 재료 제거
  3. T2T 간격 축소: 에칭으로 최종 T2T < 15nm 달성

OPC 최적화:
  - GCB 에칭 결과를 고려한 역방향 OPC
  - 에칭 후 CD/T2T 균일성 최적화
```

### EUV 성능 부스트 전략
```
성능 메트릭:
  T2T_final = T2T_printed - ΔT2T_etch
  CD_uniformity: 에칭 후 CD 3σ

OPC 목표:
  EUV 인쇄 후 에칭 전 T2T 균일성 최적화
  → 에칭 후 최종 T2T 균일성 보장
```

## OPC 툴 SMO 구현 관련성
- 에칭 후 CD 인식 OPC: GCB 에칭 모델을 OPC 비용 함수에 통합
- T2T 패터닝 전략: 해상도 한계 이하 피처의 OPC/RET 설계
- 신규 공정 통합 OPC: 에칭/CMP 등 후공정을 포함한 통합 OPC 플로우
- SKOPC 에칭 모델 모듈에서 GCB 방향성 에칭 지원 참조

## 태그
`EUV`, `patterning`, `tip_to_tip`, `GCB`, `directional_etch`, `OPC`, `metal`, `PnR`, `resolution_limit`, `SPIE`, `2025`
