# Topography Effects on High-NA EUV

## 메타데이터
- **저자**: Guzman et al.
- **연도**: 2025
- **게재지**: Proc. SPIE 13428, Advances in Patterning Materials and Processes XLII, 3054358 (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3054358

## 핵심 요약
고NA EUV 리소그래피에서 기판 토포그래피(형상)가 초점 심도(DOF)에 미치는 영향을 분석한다. 웨이퍼 레이어 스택의 토포그래피가 고NA EUV 층에 대한 DOF에 어떻게 영향을 미치는지 검토하며, OPC/SMO 설계 시 기판 토포그래피를 고려해야 하는 필요성을 제시한다.

## 주요 기여
1. **기판 토포그래피-DOF 연계**: 웨이퍼 레이어 스택 형상이 고NA EUV DOF에 미치는 영향 정량화
2. **토포그래피 인식 OPC**: 기판 형상 변동이 OPC 보정에 미치는 영향 분석
3. **고NA EUV 특화**: 0.55NA에서 토포그래피 효과가 0.33NA 대비 더 민감하게 작용하는 이유
4. **레이어별 토포그래피 최적화**: OPC/SMO에서 기판 토포그래피를 고려한 설계 가이드

## 알고리즘/수식
### 토포그래피가 DOF에 미치는 영향
```
고NA EUV DOF 예산:
  DOF_total = DOF_optical - ΔZ_topography - ΔZ_M3D - ΔZ_aberration

  DOF_optical (0.55NA): ≈ 30~50nm
  ΔZ_topography: 기판 단차에 의한 포커스 이동

토포그래피 효과 메커니즘:
  기판 단차 h_topo → 유효 포커스 위치 이동 Δf
  Δf ≈ h_topo × (n_substrate - 1) / n_substrate
  (층간 굴절률 차이에 따른 광학 경로 차이)

고NA에서 더 민감:
  DOF_0.55NA < DOF_0.33NA
  → ΔZ_topography가 DOF 예산에서 차지하는 비중 증가
  → 토포그래피 관리가 더 중요해짐
```

### 토포그래피 인식 OPC
```
토포그래피 인식 OPC:
  CD(x, y) = f(optical_image, resist, topography(x, y))

  topography(x, y): 위치별 기판 단차 맵
  → OPC 보정에 위치별 포커스 오프셋 반영

SMO와 토포그래피:
  토포그래피 변동을 SMO 공정 창 최적화에 통합
  → 더 강건한 소스 형상 도출
```

## OPC 툴 SMO 구현 관련성
- 토포그래피 인식 OPC: SKOPC에서 기판 토포그래피 맵을 OPC 입력으로 활용
- 고NA DOF 예산 관리: 0.55NA EUV OPC/SMO에서 토포그래피 요인 포함 DOF 분석
- SMO 강건성: 기판 형상 변동을 SMO 공정 창 계산에 포함
- 레이어별 최적화: 토포그래피가 특히 문제가 되는 레이어에서 SMO/OPC 강화

## 태그
`EUV`, `high_NA`, `topography`, `DOF`, `focus_budget`, `OPC`, `SMO`, `substrate`, `layer_stack`, `SPIE`, `2025`
