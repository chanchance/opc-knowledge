# Pixelated Source Polarization Optimization for High-NA EUV Lithography

## 메타데이터
- **저자**: Yu-Jin Chae, Min-Woo Kim, Da-Kyung Yu, Ji-Won Kang, Hee-Chang Ko, Michael Yeung, Seung-Woo Son, Hye-Keun Oh
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 1342419 (22 April 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3054302

## 핵심 요약
고NA EUV 리소그래피에서 각 소스 점(source pixel)별로 최적 편광각을 독립적으로 결정하는 픽셀화 소스 편광 최적화(pixelated source polarization optimization) 방법을 제안한다. 기존 방법이 소스 형상 분포 수정에 집중하면서 편광 상태를 고정했던 한계를 극복하여 NILS, nDOF, 패턴 충실도를 크게 향상시킨다.

## 주요 기여
1. **픽셀화 편광 최적화**: 각 소스 픽셀의 편광각을 개별적으로 최적화하는 새로운 방법
2. **기존 SMO 한계 극복**: 편광 고정 소스 최적화의 성능 한계를 편광 자유도 추가로 극복
3. **DRAM 패턴 성능 향상**: 복잡한 DRAM 패턴에서 NILS, nDOF 및 전반적 패턴 충실도 개선
4. **픽셀 수준 편광 맵**: 소스 평면에서 위치별 최적 편광각 분포 생성

## 알고리즘/수식
### 픽셀화 소스 편광 최적화
```
최적화 변수: {J(f_m), θ_pol(f_m)} for all source pixels m

여기서:
- J(f_m): m번째 소스 픽셀 강도
- θ_pol(f_m): m번째 소스 픽셀의 편광각 (0° ~ 180°)

이미징 모델:
I(x) = Σ_m J(f_m) · |Σ_n H_pol(f_m, f_n, θ_pol(f_m)) · M(f_n)|²

H_pol: θ_pol 의존 광학 전달 함수

비용 함수:
min_{J, θ_pol} -NILS - λ·nDOF + μ·||J||_1 (소스 희소성)

제약:
  0 ≤ J(f_m) ≤ J_max
  0° ≤ θ_pol(f_m) ≤ 180°
  Σ_m J(f_m) = P_total
```

### 기존 방법과의 차이
```
기존 소스 최적화:
  변수: {J(f_m)} only
  편광 상태: 전역 고정 (예: TE, TM, circular)

픽셀화 편광 최적화 (제안):
  변수: {J(f_m), θ_pol(f_m)} 동시 최적화
  편광 상태: 픽셀별 독립 최적화
  → 더 넓은 최적화 공간으로 성능 향상
```

### 타겟 패턴
- 복잡한 DRAM 패턴
- 고NA EUV (0.55NA) 조건

## OPC 툴 SMO 구현 관련성
- 고NA EUV SMO의 최신 편광 최적화 방향: 픽셀별 독립 편광 자유도 추가
- SKOPC SMO 소스 표현 확장: (x, y, intensity) → (x, y, intensity, pol_angle) 4차원 소스
- 비용 함수 설계: 픽셀화 편광 최적화를 위한 연속 완화(continuous relaxation) 기법
- 계산 복잡도: 2N 변수(N 소스 픽셀 × 2: 강도 + 편광각)로 SMO 최적화 스케일

## 태그
`SMO`, `EUV`, `high_NA`, `polarization_optimization`, `pixelated_source`, `NILS`, `nDOF`, `DRAM`, `0.55NA`, `SPIE`
