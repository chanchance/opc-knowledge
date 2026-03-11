# EUV APSM Mask Prospects and Challenges

## 메타데이터
- **저자**: (SPIE 12751 저자 정보)
- **연도**: 2023
- **게재지**: Proc. SPIE 12751, Photomask Technology 2023, 2688111 (2023)
- **DOI/URL**: https://doi.org/10.1117/12.2688111

## 핵심 요약
EUV 감쇠형 위상 이동 마스크(APSM, Attenuated Phase Shift Mask)의 가능성과 도전을 검토한다. APSM이 0.33NA EUV에서 28nm 피치까지 해상도를 확장할 수 있음을 보이고, 굴절률(n, k) 최적화와 재료 선택, 실현 가능성 연구를 통해 EUV APSM의 실용화 경로를 제시한다.

## 주요 기여
1. **EUV APSM 해상도 확장**: 0.33NA EUV에서 28nm 피치 달성 가능성 검증
2. **재료 (n, k) 최적화**: 최적 APSM 흡수층 광학 상수 선택
3. **M3D 완화 효과**: APSM 위상 이동으로 마스크 3D 효과 일부 완화
4. **실현 가능성 연구**: 제조 가능한 APSM 재료 및 공정 경로 분석

## 알고리즘/수식
### EUV APSM 이미징 원리
```
APSM 마스크 특성:
  반사율: R_att (부분 반사, 예: 10~20%)
  위상 이동: φ_shift ≈ 180° (반전상 위상)
  목표: 패턴 경계에서 전기장 부분 상쇄 → 이미지 대비 향상

APSM vs 이진 마스크 (TaBN):
  이진 마스크: R_att = 0% (완전 흡수)
  APSM: R_att > 0%, φ ≈ π → 반사광 위상 반전

이미지 대비 향상:
  NILS_APSM > NILS_binary (동일 피치)
  → 더 낮은 도즈에서 안정적 패터닝 가능

28nm 피치 달성:
  k1_eff = NA × pitch / λ = 0.33 × 28nm / 13.5nm ≈ 0.685
  APSM으로 k1 < 0.7 영역 패터닝 향상
```

### (n, k) 최적화
```
APSM 재료 최적화:
  목표: R_att ≈ 10~15%, φ_shift ≈ 180° at λ=13.5nm

  최적화 변수: (n_abs, k_abs, t_abs)
  제약: MRC 충족, M3D 효과 최소화

  후보 재료: RuO₂, Mo₂N, TiN 등
  → 각 재료별 (n, k) 13.5nm에서 측정 후 최적 선택
```

## OPC 툴 SMO 구현 관련성
- APSM 마스크 OPC 모델: SKOPC OPC/SMO 모듈에서 APSM 마스크 타입 지원
- APSM 위상 효과 모델링: 위상 이동 항을 OPC 광학 모델에 통합
- SMO와 APSM 결합: APSM 마스크에 최적화된 소스 형상 도출
- EUV 마스크 타입 분기: TaBN / low-n / APSM 별 OPC 모델 분기 설계

## 태그
`EUV`, `APSM`, `attPSM`, `phase_shift_mask`, `28nm_pitch`, `n_k_optimization`, `M3D`, `resolution`, `OPC`, `SMO`, `SPIE`, `2023`
