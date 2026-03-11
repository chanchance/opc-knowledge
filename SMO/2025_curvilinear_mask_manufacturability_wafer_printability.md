# The Exploration of Curvilinear Mask Manufacturability and Wafer Printability

## 메타데이터
- **저자**: (SPIE 13425 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 1342512 (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3050611

## 핵심 요약
곡선형 마스크의 제조 가능성(manufacturability)과 웨이퍼 인쇄 가능성(printability)을 동시에 탐구한다. MBMW를 이용한 곡선형 마스크 제조 품질과 그 결과가 웨이퍼에서 어떻게 인쇄되는지를 측정하고, MRC(마스크 규칙 검사) 준수와 패터닝 성능 간의 트레이드오프를 분석한다.

## 주요 기여
1. **곡선형 마스크 제조 품질 평가**: MBMW 제조 곡선형 마스크의 CD/엣지 품질 측정
2. **웨이퍼 인쇄 가능성 검증**: 곡선형 마스크로 인쇄된 웨이퍼 패턴 품질 평가
3. **MRC-패터닝 트레이드오프**: 제조 규칙 완화 시 패터닝 성능 이익과 제조 리스크
4. **OPC-MRC 공동 최적화**: 곡선형 OPC 결과의 MRC 준수와 웨이퍼 품질 동시 최적화

## 알고리즘/수식
### 곡선형 마스크 제조-인쇄 분석
```
곡선형 마스크 제조 파라미터:
  MBMW (Multi-Beam Mask Writer):
    빔 크기: ~6nm (마스크 상)
    픽셀 크기: ≤2nm (마스크 상)
    → 곡선형 형상 충실도 높음

  제조 품질 지표:
    MCD (Mask CD): 목표 대비 편차
    MER (Mask Edge Roughness): 마스크 에지 거칠기
    MC (Mask Circularity): 곡선형 에지 평활도

MRC (Mask Rule Check):
  곡선형 MRC 규칙:
    min_radius: 최소 곡률 반경 ≥ R_min
    min_feature: 최소 피처 크기 ≥ W_min
    min_space: 최소 간격 ≥ S_min
  MRC 위반 → 제조 불가 또는 품질 저하
```

### 제조-인쇄 상관관계
```
마스크 제조 오차 → 웨이퍼 CD 영향:
  MEEF (Mask Error Enhancement Factor):
    ΔCD_wafer = MEEF × ΔCD_mask × (1/M)
    곡선형 마스크에서 MEEF 변화 가능

웨이퍼 인쇄 품질:
  CD_wafer = f(CD_mask, MEEF, process)
  LER_wafer = g(MER_mask, MEEF, resist)

MRC 완화 효과:
  더 엄격한 MRC → 더 단순한 곡선 → 더 나쁜 패터닝
  더 관대한 MRC → 더 복잡한 곡선 → 더 좋은 패터닝
  최적점: 패터닝 이득 > 제조 리스크
```

## OPC 툴 SMO 구현 관련성
- 곡선형 OPC-MRC 통합: SKOPC ILT/곡선형 OPC에서 MRC 준수와 인쇄 품질 동시 최적화
- 제조 가능한 곡선형 OPC: 제조 가능한 곡선형 형상을 생성하는 OPC 알고리즘
- MRC 인식 ILT: ILT 최적화에 MRC 제약 조건을 페널티 항으로 통합
- 마스크-웨이퍼 품질 연계: 마스크 제조 품질 시뮬레이션으로 웨이퍼 결과 예측

## 태그
`curvilinear`, `mask_manufacturability`, `printability`, `MRC`, `MBMW`, `OPC`, `ILT`, `MEEF`, `CD`, `LER`, `SPIE`, `2025`
