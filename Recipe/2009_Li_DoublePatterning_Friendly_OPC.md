# Double-Patterning-Friendly OPC

## 메타데이터
- **저자**: Xiaohai Li, Gerry Luk-Pat, Chris Cork, Levi Barnes, Kevin Lucas
- **소속**: Mentor Graphics
- **연도**: 2009
- **게재지**: Proc. SPIE 7274, Optical Microlithography XXII, 727414
- **DOI/URL**: https://doi.org/10.1117/12.815175

## 핵심 요약
32nm half-pitch 이하를 위한 Double Patterning Technology(DPT)에서 OPC를 적용하는 방법론을 제시한다. LELE(Litho-Etch-Litho-Etch) 방식으로 분해된 두 레이아웃에 각각 OPC를 적용할 때 발생하는 새로운 도전 과제들 — 큰 litho-etch bias, 두 패터닝 레이어의 공정 변수, 그리고 오버랩 영역에서의 패턴 상호작용 — 을 체계적으로 해결한다.

## 주요 기여
1. **DPT OPC 플로우 확립**: 레이아웃 decomposition → 각 mask OPC → 패터닝 순서 고려 통합 플로우
2. **큰 litho-etch bias 처리**: 기존 OPC 대비 훨씬 큰 bias를 수용하는 확장된 보정 범위
3. **공정 변수 쌍 관리**: 두 패터닝 레이어 각각의 공정 변수 집합과 상호 관계 모델링
4. **오버랩 영역 최적화**: LELE 오버랩 영역에서의 패턴 상호작용 고려한 OPC 보정
5. **패터닝 순서 최적화**: 어느 mask를 먼저 노광할지에 따른 공정 영향 분석

## Recipe/Flow 상세
```
[Double-Patterning-Friendly OPC Flow]
1. 레이아웃 분해(Decomposition):
   - 원본 디자인 → Mask A + Mask B (conflict-free 분리)
   - Color assignment 및 spacing rule 검증
2. 각 Mask 독립 OPC:
   - Mask A: OPC + SRAF (Mask B 패턴 존재 고려)
   - Mask B: OPC + SRAF (Mask A 패턴 존재 고려)
3. 오버랩 영역 처리:
   - 두 mask 패턴이 근접/교차하는 영역 식별
   - 상호 litho 영향 시뮬레이션
   - 보정값 조정
4. 패터닝 순서 결정 및 최종 검증:
   - Overlay error 허용 범위 내 공정 마진 확인
   - Full-chip ORC (Optical Rule Check)
```

### 핵심 파라미터
- **적용 노드**: 32nm half-pitch 이하
- **DPT 방식**: LELE (Litho-Etch-Litho-Etch)
- **Litho-etch bias**: 기존 OPC보다 훨씬 큰 값 처리 필요
- **오버랩 영역**: 두 mask 간 relative placement 오차 고려

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: 다중 패터닝을 위한 OPC 플로우 확장 시 참고
- **Double patterning 지원**: SKOPC에 LELE/SADP용 레이어 분리 및 다중 mask OPC 기능 추가 로드맵에 활용
- `recipes/example_arfimm.yaml`: 28nm 노드에서 DPT 적용 시 recipe 파라미터 참고
- **OPC Recipe 파라미터**: `etch_bias`, `litho_etch_bias_scale` 파라미터의 DPT 확장값 설정 참고

## 태그
`Recipe`, `SPIE`, `Double Patterning`, `LELE`, `DPT`, `OPC`, `32nm`, `Litho-Etch`, `Multi-Patterning`, `Overlay`
