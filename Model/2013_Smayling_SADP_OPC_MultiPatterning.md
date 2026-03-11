# Double Patterning from Design Enablement to Verification

## 메타데이터
- **저자**: Smayling, M. C. et al. (Tela Innovations / imec)
- **연도**: 2012
- **게재지**: Proc. SPIE 8166, Photomask Technology 2011
- **DOI/URL**: https://doi.org/10.1117/12.898895
- **인용수**: ~80

## 핵심 요약
20nm 콘택, 비아, 하위 메탈 레이어를 위한 LELE(Litho-Etch-Litho-Etch) 이중 패터닝 기술의 설계 인에이블먼트부터 검증까지 전체 플로우를 다룬다. LELE의 고유한 설계·공정 특성을 분석하고, 각 노광의 OPC 모델과 오버레이 오차가 최종 패턴 품질에 미치는 영향을 정량화한다. SADP 대비 LELE의 장단점 및 노드별 적용 전략을 제시한다.

## 주요 기여
1. LELE 이중 패터닝의 설계→OPC→검증 전체 플로우 체계화
2. 오버레이 오차와 각 노광 OPC 모델의 결합 영향 분석
3. 20nm 노드 콘택/비아 레이어에서 LELE 적용 가이드라인
4. LELE vs. SADP 경쟁 기술 비교 분석
5. 패턴 분해(coloring) 규칙 기반 설계 최적화 방법론

## 모델 수식/아키텍처

**LELE 이중 노광 모델:**
```
I_total(x) = I_mask1(x) + I_mask2(x)  [비간섭 합산]
CD_final = f(I_mask1, I_mask2, overlay_error)
```

**오버레이 오차 영향:**
```
CD_space(overlay) = CD_space_nominal - |overlay_x| - |overlay_y|
EPE_overlay = ∂EPE/∂overlay · Δoverlay
```

**각 마스크 OPC 모델:**
```
EPE_mask1 = Litho_Model(mask1_OPC, optical1, resist)
EPE_mask2 = Litho_Model(mask2_OPC, optical2, resist)
EPE_total ≈ EPE_mask1 ⊕ EPE_mask2 ⊕ EPE_overlay
```

**LELE 공정 윈도우 (오버레이 포함):**
```
PW_LELE = PW_single × f(overlay_budget)
overlay_budget = 3σ_overlay = k · CD / (MEEF · M)
```

**패턴 분해 (Coloring) 규칙:**
```
min_spacing_same_color > pitch_min
→ 두 마스크로 분리하여 각 마스크의 최소 피치 2× 완화
```

## 모델 유형
- [x] 광학 모델 (이중 노광 광학 모델)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc LELE OPC 구현: 두 마스크 각각 독립 OPC 후 오버레이 영향 검증
- 각 마스크 OPC: 단일 노광 OPC와 동일하나, 인접 마스크 패턴 상호작용 고려
- 이중 패터닝 검증: 오버레이 범위 전체에서 EPE 평가
- 패턴 분해 후 각 서브셋에 독립 OPC 모델 적용
- 28/20nm: LELE; 14/10nm: SAQP; 7nm 이하: EUV로 전환

## 참고문헌
- Yu, P. et al., "True Process Variation Aware OPC" (2007)
- Sturtevant, J. et al., "Roadmap to sub-nanometer OPC" (2012)
- ITRS multi-patterning roadmap

## 태그
`Model`, `SPIE`, `DoublePatterning`, `LELE`, `MultiPatterning`, `OPC`, `Overlay`, `20nm`, `2012`
