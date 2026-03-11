# Improving Process Window and Resolution Through Source Polarization in High-NA EUV

## 메타데이터
- **저자**: Yu-Jin Chae, Min-Woo Kim, Da-Kyung Yu, Seung-woo Son, Michael Yeung, Hye-Keun Oh
- **연도**: 2024
- **게재지**: Proc. SPIE 13216, Photomask Technology 2024, 132162M (20 November 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3037370

## 핵심 요약
고NA EUV 리소그래피에서 편광 조명(polarized illumination)이 패턴 충실도와 해상도를 향상시키는 효과를 체계적으로 분석한다. NILS와 nDOF의 두 핵심 성능 메트릭에 대한 편광의 영향을 정량화하고, 소스 최적화에 편광을 통합하여 공정 창을 확장하는 방법을 제시한다.

## 주요 기여
1. **편광 소스 최적화 효과 정량화**: 편광 조명이 NILS 및 nDOF에 미치는 영향 체계적 분석
2. **공정 창 확장**: 소스 최적화에 편광 통합으로 전체 이미징 성능 향상
3. **고NA EUV 편광 분석**: 0.55NA 고NA 조건에서 편광 효과의 특수성 분석
4. **실용적 소스 설계 가이드**: 편광 상태를 고려한 최적 소스 형상 설계 지침

## 알고리즘/수식
### 편광 소스 최적화 프레임워크
```
TM(TE) 편광 이미징 모델:
I(x) = Σ_{m,n} J(f_m) · |H(f_m, f_n)|² · M(f_n) · P_pol(f_m)

여기서:
- J(f_m): 소스 점 m의 강도
- H: 전사 함수 (렌즈 PSF)
- M(f_n): 마스크 회절 스펙트럼
- P_pol: 편광 상태 인수 (TE/TM 기여)

고NA EUV (0.55NA)에서 편광 효과:
- TE(s) 편광: 높은 NA에서 유리 (대비 향상)
- TM(p) 편광: 높은 NA에서 불리 (대비 감소)
- 최적 편광: 패턴 방향에 따라 TE 우선
```

### 소스 최적화에 편광 통합
```
편광 인식 소스 최적화:
min_{J, pol_angle} Cost(NILS, nDOF)

Cost = -w₁·NILS - w₂·nDOF + w₃·source_constraint

제약: Σ J(f_m) = P_total (총 광파워 보존)
      0 ≤ pol_angle(f_m) ≤ π (편광각 범위)
```

### 성능 메트릭
- **NILS**: 정규화 이미지 대수 기울기 (해상도 척도)
- **nDOF**: 정규화 심도 (초점 허용 범위)

## OPC 툴 SMO 구현 관련성
- 고NA EUV SMO에서 편광 최적화 필수화: 단순 강도 분포 최적화를 넘어 편광 상태 공동 최적화
- SKOPC SMO 모듈의 고NA EUV 지원 시 편광 자유도 추가 필요
- 소스 모델 확장: J(x,y) → J(x,y, pol_angle) 형태로 소스 표현 확장
- 비용 함수: NILS + nDOF 기반 편광 인식 비용 함수 설계 참조

## 태그
`SMO`, `EUV`, `high_NA`, `polarization`, `source_optimization`, `NILS`, `nDOF`, `process_window`, `0.55NA`, `SPIE`
