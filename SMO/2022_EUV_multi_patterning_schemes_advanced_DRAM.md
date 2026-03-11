# EUV Based Multi-Patterning Schemes for Advanced DRAM Nodes

## 메타데이터
- **저자**: (SPIE 12055 저자 정보)
- **연도**: 2022
- **게재지**: Proc. SPIE 12055, Optical Microlithography XXXV, 1205503 (2022)
- **DOI/URL**: https://doi.org/10.1117/12.2615644

## 핵심 요약
첨단 DRAM 노드를 위한 EUV 기반 다중 패터닝(multi-patterning) 방식을 제시한다. 두 개의 EUV 마스크로 단순 경사 라인-공간 패턴을 사용하여 허니콤(honeycomb) 배열 컨택 홀 및 기둥 패턴을 구현하는 이중 패터닝 기법을 시연한다.

## 주요 기여
1. **EUV 이중 패터닝 DRAM 적용**: 두 EUV 마스크를 활용한 허니콤 패턴 구현
2. **경사 라인-공간 패턴**: 단순 마스크 설계로 복잡한 2D 패턴 생성
3. **DRAM 첨단 노드 솔루션**: EUV 다중 패터닝으로 DRAM 스케일링 가능성 제시
4. **오버레이 인식 최적화**: 두 노출 간 오버레이 오차를 고려한 공정 최적화

## 알고리즘/수식
### EUV 이중 패터닝 허니콤 방식
```
허니콤 컨택 홀 이중 패터닝:
  마스크 1: 경사 라인-공간 (각도 θ₁)
  마스크 2: 경사 라인-공간 (각도 θ₂ = θ₁ + 60°)

  교차 노출 결과:
    I_total = I_mask1 ∩ I_mask2
    → 허니콤 컨택 홀 어레이 형성

패턴 피치 관계:
  허니콤 피치 = f(라인-공간 피치, 각도 θ)
  최적 각도: θ = 30° ~ 60° (허니콤 대칭)

오버레이 영향:
  CD_variation = f(ΔOverlay_x, ΔOverlay_y)
  → SMO/OPC에서 오버레이 공차 고려 필요
```

### 다중 패터닝 SMO 확장
```
다중 패터닝 비용 함수:
  Cost_MP = Σ_mask Σ_i [||CD_i - CD_target||²]
           + w_overlay · ||ΔOverlay||²

마스크별 소스 최적화:
  J₁*, J₂* = argmin_{J₁, J₂} Cost_MP
  → 두 노출 간 최적 소스 형상 결정
```

## OPC 툴 SMO 구현 관련성
- 다중 패터닝 SMO: SKOPC에서 두 노출을 동시에 고려한 SMO 확장
- 오버레이 인식 OPC: 두 마스크 간 오버레이 공차를 OPC 비용 함수에 통합
- DRAM 패터닝 솔루션: DRAM BLP/SNLP 외 허니콤 이중 패터닝 지원
- 경사 패턴 SMO: 비-맨해튼 패턴에 최적화된 소스 형상 도출

## 태그
`EUV`, `multi_patterning`, `double_patterning`, `DRAM`, `honeycomb`, `contact_hole`, `overlay`, `SMO`, `OPC`, `SPIE`
