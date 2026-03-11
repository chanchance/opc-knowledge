# Model-Based OPC Using the MEEF Matrix II

## 메타데이터
- **저자**: Junjiang Lei, Le Hong, George Lippincott, James Word
- **연도**: 2014
- **게재지**: Proc. SPIE 9052, Optical Microlithography XXVII, 90520N
- **DOI/URL**: https://doi.org/10.1117/12.2046635
- **인용수**: ~40

## 핵심 요약
기술 노드 축소로 세그먼트 간 상호작용이 강해져 단일 세그먼트 EPE 기반 피드백 튜닝만으로는 우수한 패턴 충실도와 합리적 TAT를 달성할 수 없게 된 문제를 해결한다. 행렬 OPC(matrix OPC) 개념과 알고리즘을 따르는 이웃 인식 피드백 컨트롤러(neighbor-aware feedback controller)를 전체 칩 OPC에 적용하는 방법을 제시한다.

## 주요 기여
1. Cross-MEEF를 활용한 이웃 세그먼트 영향 통합 피드백 제어기
2. 전체 칩 수준 행렬 OPC 적용을 위한 효율적 알고리즘
3. 강한 세그먼트 간 상호작용 환경(저 k1)에서의 수렴 개선
4. 2002년 MEEF Matrix I의 실용적 전체 칩 확장

## Recipe/Process Flow 상세

### MEEF 행렬 기반 OPC 이론
```
기존 OPC (단일 세그먼트 피드백):
  Δmask_i = gain_i × EPE_i
  문제: 이웃 세그먼트 영향 무시 → 저 k1에서 느린 수렴/발산

행렬 OPC (MEEF Matrix):
  EPE = A × Δmask   (선형 관계)
  여기서:
    EPE = [epe_1, epe_2, ..., epe_N]  (모든 시뮬레이션 포인트)
    Δmask = [δ_1, δ_2, ..., δ_M]      (모든 세그먼트 이동량)
    A = MEEF 행렬 (N×M)
      A_ij = ∂epe_i/∂mask_j   (cross-MEEF)

최적 이동량 계산:
  Δmask = A⁺ × EPE_target
  여기서 A⁺ = pseudoinverse of A
  또는: Δmask = (AᵀA + λI)⁻¹ × Aᵀ × EPE  (정규화)
```

### 이웃 인식 피드백 컨트롤러
```
1. 국소 MEEF 행렬 구성
   - 각 세그먼트에 대해 영향 반경 내 이웃 세그먼트 식별
   - 부분 MEEF 행렬 계산 (전체 행렬 대신 희소 행렬)
   - 계산 효율성: O(N²) → O(N×K) (K = 평균 이웃 수)

2. 이터레이션당 세그먼트 업데이트
   For each iteration:
     a) 리소그래피 시뮬레이션 → EPE 계산
     b) 국소 MEEF 행렬 적용
        Δmask_i = Σ_j (A_ij)⁺ × EPE_j  (이웃 j 포함)
     c) 댐핑 팩터 적용
     d) 마스크 업데이트

3. 전체 칩 확장
   - 계층적 처리로 메모리/런타임 관리
   - 희소 행렬 연산으로 효율화
```

### 성능 결과
```
저 k1 리소그래피 (강한 상호작용 환경):
  기존 OPC: 느린 수렴, 일부 패턴 발산 위험
  MEEF Matrix OPC: 빠른 수렴, 안정적
  이터레이션 감소: ~30-50%
  EPE 정확도: 개선 (이웃 효과 반영)
```

### 파라미터
```
영향 반경 (interaction radius): OPC 세그먼트 간 최대 거리
정규화 파라미터 λ: 수치 안정성 제어
댐핑 팩터: 과보정 방지
```

## OPC 툴 구현 관련성
- **SKOPC 수렴 개선**: `skopc/modeling/model_opc.py`의 이터레이션 루프에 MEEF 행렬 기반 피드백 적용 가능
- **Jacobian 행렬**: `skopc/core/litho_engine.py`에서 강도 분포 Jacobian 계산으로 MEEF 행렬 구성
- **희소 행렬**: 전체 칩 수준 효율적 처리를 위한 scipy.sparse 활용
- **Mentor Graphics 시리즈**: MEEF Matrix I (2002) → II (2014) → III (2024) 시리즈

## 참고문헌
- Proc. SPIE 9052, Optical Microlithography XXVII (2014)
- 저자 소속: Mentor Graphics Corp.
- 선행: Model-based OPC using the MEEF matrix (SPIE 4889, 2002) — Cobb, Granik
- 후속: Model-based OPC using the MEEF matrix III (SPIE 12954, 2024)

## 태그
`Recipe`, `SPIE`, `MEEFMatrix`, `MatrixOPC`, `ModelBasedOPC`, `CrossMEEF`, `NeighborAware`, `ConvergenceControl`, `MentorGraphics`, `LowK1`
