# Source Mask Optimization (SMO) at Full Chip Scale Using Inverse Lithography Technology Based on Level Set Methods

## 메타데이터
- **저자**: Linyong Pang, Yong Liu, Douglas Abrams
- **연도**: 2009
- **게재지**: Proc. SPIE 7520, Lithography Asia 2009
- **DOI/URL**: https://doi.org/10.1117/12.843578
- **인용수**: ~80

## 핵심 요약
ILT(Inverse Lithography Technology) 기반의 레벨 셋(Level Set) 방법론을 소스-마스크 동시 최적화(SMO)로 확장하여 단일 클립에서 전체 칩 스케일까지 SMO를 구현하는 방법론을 제시한다. 조명(source)과 마스크를 동시에 최적화함으로써 각각을 독립적으로 최적화하는 접근법 대비 공정 윈도우를 크게 향상시킨다.

## 주요 기여
1. ILT 기반 레벨 셋 방법의 SMO로의 확장 (소스+마스크 동시 최적화)
2. 단일 클립에서 전체 칩 스케일까지의 SMO 확장성 시연
3. 순차적 소스-마스크 최적화 대비 동시 최적화의 우위 증명
4. 픽셀화된 자유형(freeform) 조명 + 연속 마스크 전송 함수 동시 최적화

## Recipe/Process Flow 상세

### SMO의 기본 원리
```
기존 접근법 (순차적):
  Step 1: 소스 최적화 (Source Optimization, SO)
  Step 2: 고정 소스에서 마스크 최적화 (OPC/ILT)
  한계: 두 단계 간 상호의존성 무시 → 최적해 미달

동시 SMO:
  min_{S, M} F(S, M)
  = min_{S, M} Σ_k ||I_k(S, M) - I_target||²
                + λ_S R(S) + λ_M R(M)

  S: 소스 강도 분포 (픽셀화된 freeform 조명)
  M: 마스크 투과율 (연속 또는 이진)
  I_k: k번째 공정 조건에서의 이미지
  R: 정규화항 (소스/마스크 복잡도 제어)
```

### ILT 기반 레벨 셋 SMO 알고리즘
```
레벨 셋(Level Set) 방법:
  마스크 경계를 암묵적 함수 φ(x,y)로 표현:
    M(x,y) = H(φ(x,y))  (H: Heaviside 함수)
  경계 이동: ∂φ/∂t = -∇F · |∇φ|
  장점: 위상 변화(topology change) 자연스럽게 처리

SMO 알고리즘:
  초기화: 초기 마스크 M_0, 초기 소스 S_0
  이터레이션:
    1. 마스크 그래디언트 계산:
       ∂F/∂φ = ∂F/∂M · δ(φ)
    2. 소스 그래디언트 계산:
       ∂F/∂S_pq (각 소스 픽셀에 대한 편미분)
    3. 마스크 업데이트: φ ← φ - α_M · ∂F/∂φ
    4. 소스 업데이트: S ← S - α_S · ∂F/∂S
       (소스 제약: S_pq ≥ 0, Σ S_pq = 1)
  수렴: 에너지 F 변화가 임계값 이하
```

### 전체 칩 확장성
```
클립 기반에서 전체 칩으로:
  1. 레이아웃을 대표 클립으로 분할
  2. 각 클립별 SMO 실행 → 클립별 마스크 패치
  3. 클립 간 마스크 패치 통합 (경계 일치)
  4. 통합 소스: 모든 클립의 최적 소스를 통합하여 단일 소스 산출

컴퓨팅 효율화:
  - 레벨 셋 방법의 sparse 표현 활용
  - GPU 병렬화
  - 계층적 최적화 (coarse → fine)
```

### 성능 결과
```
순차적 SO+OPC 대비 동시 SMO:
  공정 윈도우 (DOF × EL): 동시 SMO 우세
  마스크 복잡도: 비슷하거나 낮음
  런타임: 증가하나 허용 범위

응용 노드: 22nm급 ArF 액침 리소그래피
  패턴: 메탈 레이어, 폴리 게이트 레이어
  k1: 0.25~0.30 극저 k1 환경
```

## OPC 툴 구현 관련성
- **SKOPC SMO 모듈**: `skopc/smo/` 소스-마스크 동시 최적화 기반으로 레벨 셋 SMO 구현 참조
- **레벨 셋 방법**: OpenILT(`skopc/modeling/openilt_adapter.py`)와 연동하여 SMO 확장 가능
- **소스 표현**: 픽셀화된 freeform 소명을 `skopc/smo/source_optimizer.py`에서 파라미터로 관리
- **비용 함수**: EPE 기반 + 공정 윈도우 최대화 비용함수 설계

## 참고문헌
- Proc. SPIE 7520, Lithography Asia 2009
- 저자 소속: Luminescent Technologies (now acquired)
- 관련: Source-mask co-optimization using level set methods (SPIE 7488, 2009)
- 관련: Full-chip source and mask optimization (SPIE 7973, 2011)
- 관련: An innovative SMO method for extending low k1 imaging (SPIE 7140, 2008)

## 태그
`Recipe`, `SPIE`, `SMO`, `SourceMaskOptimization`, `ILT`, `LevelSet`, `FullChip`, `Freeform`, `ProcessWindow`, `22nm`, `2009`
