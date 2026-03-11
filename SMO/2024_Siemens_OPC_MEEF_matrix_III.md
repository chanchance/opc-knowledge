# Model-Based OPC Using the MEEF Matrix III

## 메타데이터
- **저자**: Siemens EDA (Mentor/Calibre 팀)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, Optical and EUV Nanolithography XXXVII, 1295418 (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010562

## 핵심 요약
Siemens EDA의 Calibre MatrixOPC 기능을 소개한다. MEEF(Mask Error Enhancement Factor) 행렬 기반 모델 OPC 방법론의 3번째 연구로, 고NA EUV 및 저-k1 패터닝에서 마스크 CD 오차가 웨이퍼에 미치는 영향을 행렬 형식으로 정밀하게 모델링하여 OPC 보정 품질을 향상시킨다.

## 주요 기여
1. **MEEF 행렬 OPC**: 단순 스칼라 MEEF 대신 행렬 형태로 인접 피처 간 상호작용 모델링
2. **Calibre MatrixOPC**: Siemens EDA의 상용 구현으로 실 생산 적용 가능
3. **고NA EUV 적용**: MEEF 행렬이 중요해지는 0.55NA EUV 패터닝에 적용
4. **OPC 보정 품질 향상**: 기존 스칼라 MEEF OPC 대비 정확도 개선

## 알고리즘/수식
### MEEF 행렬 OPC 방법론
```
기존 스칼라 MEEF:
  MEEF = ΔCD_wafer / ΔCD_mask × (1/M)
  단순화: 단일 피처의 마스크 오차 웨이퍼 증폭

MEEF 행렬:
  MEEF_ij = ∂CD_wafer_i / ∂CD_mask_j × (1/M)
  → 피처 j의 마스크 CD 변화가 피처 i의 웨이퍼 CD에 미치는 영향
  → 비대각 성분: 인접 피처 간 광학 결합 효과

MatrixOPC 보정:
  ΔOPC = MEEF_matrix^{-1} × EPE_target
  → 행렬 역산으로 최적 OPC 보정값 결정
  → 인접 피처 상호작용을 명시적으로 보상
```

### 고NA EUV에서 MEEF 행렬 중요성
```
0.55NA EUV:
  해상도 향상 → 인접 피처 간 광학 결합 증가
  MEEF 비대각 성분 증가
  → 스칼라 MEEF OPC의 한계 명확해짐
  → MEEF 행렬 OPC 필요성 증가

성능 개선:
  EPE_3σ 감소: MEEF 행렬 OPC > 스칼라 OPC
  특히 밀집 패턴 영역에서 개선 두드러짐
```

## OPC 툴 SMO 구현 관련성
- MEEF 행렬 OPC: SKOPC Calibre 호환 OPC 엔진에서 MatrixOPC 방법론 채택 가능
- 인접 피처 상호작용: 밀집 EUV 패턴에서 인접 세그먼트 간 MEEF 행렬 적용
- 고NA EUV OPC: 0.55NA에서 MEEF 행렬 OPC의 정확도 이점 활용
- SMO 연계: MEEF 행렬을 통해 마스크 제조 오차가 웨이퍼에 미치는 영향 SMO에 통합

## 태그
`OPC`, `MEEF`, `matrix_OPC`, `Siemens`, `Calibre`, `MatrixOPC`, `EUV`, `high_NA`, `model_based_OPC`, `SPIE`, `2024`
