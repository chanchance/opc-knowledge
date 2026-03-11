# RuleLearner: OPC Rule Extraction From Inverse Lithography Technique Engine

## 메타데이터
- **저자**: Ziyang Yu, Su Zheng, Wenqian Zhao, Shuo Yin, Xiaoxiao Liang, Guojin Chen, Yuzhe Ma, Bei Yu, Martin D. F. Wong
- **연도**: 2025 (2024년 수락)
- **게재지/학회**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD), Vol. 44, Issue 5, pp. 1915-1927
- **DOI/URL**: https://ieeexplore.ieee.org/document/10753456/ (DOI: 10.1109/TCAD.2024.3499909)
- **인용수**: N/A (2025 신규)

## 핵심 요약
RuleLearner는 역리소그래피 기술(ILT) 엔진이 생성한 보정 패턴에서 해석 가능한 OPC 규칙을 자동으로 추출하는 프레임워크다. 전통적인 수동 규칙 정의의 한계를 극복하여 ILT 최적화 결과에서 직접 규칙을 학습하며, SRAF 생성과 모델 기반 OPC를 실제 산업 시나리오에서 통합적으로 처리한다. 맞춤형 자연 그래디언트 최적화로 규칙 값 분포를 정제하고, 다양한 복잡한 디자인 패턴에서 최고 수준의 리소그래피 성능과 계산 효율성을 달성한다.

## 주요 기여
- **ILT 기반 자동 규칙 추출**: ILT 엔진 최적화 결과에서 반복적 보정 패턴을 자동 추출
- **해석 가능한 규칙 생성**: 엔지니어가 이해하고 수정할 수 있는 형태의 OPC 규칙
- **SRAF+OPC 통합**: SRAF 생성과 모델 기반 OPC를 단일 프레임워크로 통합
- **자연 그래디언트 최적화**: 비선형성과 로컬-전역 성능 트레이드오프를 고려한 규칙 최적화

## Recipe/Process Flow 상세

### RuleLearner OPC 규칙 추출 플로우

```
입력: 설계 레이아웃 패턴 집합 {T_1, T_2, ..., T_N}
        ↓
[1단계: ILT 엔진 실행]
  각 패턴 T_i에 대해 수치 ILT 최적화:
  M_i* = argmin_{M} L_litho(F(M), T_i)
  → ILT 최적 마스크 집합 {M_1*, ..., M_N*} 생성
        ↓
[2단계: 보정 패턴 분석]
  각 (T_i, M_i*) 쌍에서:
  - 에지 이동량 분석: Δe_j = M_i*(e_j) - T_i(e_j)
  - 패턴 유형 분류: 라인엔드, 2D 코너, 좁은 간격 등
  - SRAF 배치 패턴 추출: 위치, 크기, 개수
  반복 패턴 클러스터링 (유사 보정 그룹화)
        ↓
[3단계: 규칙 파라미터 초기화]
  클러스터에서 초기 규칙 파라미터 추출:
  규칙 형태:
  if (패턴_유형 = X) and (간격 ∈ [d_min, d_max]):
    에지 이동 = f(간격, 선폭, ...)
    SRAF 배치 = g(위치, 크기, ...)
        ↓
[4단계: 자연 그래디언트 최적화]
  규칙 파라미터 θ 최적화:
  min_θ L(R(θ), {T_i, M_i*})

  자연 그래디언트 업데이트:
  θ_{t+1} = θ_t - η · F(θ_t)^{-1} · ∇_θ L(θ_t)
  F(θ): 피셔 정보 행렬 (규칙 파라미터 공간의 기하학 고려)
        ↓
[5단계: 규칙 검증 및 적용]
  - 새로운 패턴에 규칙 적용
  - 리소그래피 시뮬레이션으로 검증
  - 규칙 기반 OPC 실행 (고속)
        ↓
최종 OPC 규칙 집합 (Rule Set) 출력
```

### OPC 규칙 구조 (추출된 규칙 예시)

```yaml
# RuleLearner로 추출된 OPC 규칙 형식 예시
opc_rules:
  line_end_pullback:
    condition:
      pattern_type: "line_end"
      length_range: [60, 200]  # nm
    correction:
      pullback_amount: 35      # nm (학습된 값)
      serif_size: 20           # nm

  narrow_space_bias:
    condition:
      pattern_type: "space"
      space_range: [50, 80]   # nm
    correction:
      inner_bias: -8          # nm
      outer_bias: 5           # nm

  sraf_placement:
    condition:
      isolation_range: [100, 400]  # nm
    sraf:
      width: 32               # nm
      offset_from_main: 80   # nm
      max_count: 2
```

### 자연 그래디언트 최적화 상세
일반 경사 하강과의 차이:
- **일반 그래디언트**: 유클리드 거리 기반 파라미터 업데이트
- **자연 그래디언트**: 피셔 정보 행렬로 파라미터 공간의 기하학 고려
  → 비선형 규칙 파라미터 공간에서 더 효율적 수렴
  → 로컬 최적해 함정 회피 능력 향상

### 성능 결과
- 다양한 복잡한 디자인 패턴에서 검증
- 최고 수준 리소그래피 성능 달성
- 자동 추출 규칙이 수동 정의 규칙보다 우수하거나 동등
- 계산 효율성: 수치 ILT 대비 대폭 빠른 규칙 기반 OPC 실행

## OPC 툴 구현 관련성
RuleLearner는 SKOPC의 rule_opc.py 모듈 핵심 참조:
- **자동 규칙 생성**: SKOPC rule_opc.py의 OPC 규칙을 수동 정의 대신 RuleLearner로 자동 생성
- **ILT 기반 규칙 학습**: SKOPC의 수치 OPC 결과에서 재사용 가능한 규칙 자동 추출
- **SRAF 규칙 통합**: SRAF 배치 규칙을 OPC 규칙과 통합한 단일 레시피 파일 생성
- **YAML 레시피 연동**: 추출된 규칙을 SKOPC의 YAML 레시피 형식으로 자동 변환
- **자연 그래디언트**: rule_opc.py의 규칙 파라미터 최적화 알고리즘 개선에 적용

## 참고문헌 (핵심)
- Kahng et al., "VLSI Physical Design: From Graph Partitioning to Timing Closure" (2011)
- Amari, "Natural Gradient Works Efficiently in Learning" (1998)
- Chen et al., "DiffOPC" (ICCAD 2024)
- LithoBench (NeurIPS 2023)
- Cobb, "Fast pixel-based mask optimization for inverse lithography" (JM3 2006)

## 태그
`RuleLearner`, `OPC Rule Extraction`, `ILT`, `SRAF`, `Natural Gradient`, `Rule-based OPC`, `Automated Rule Generation`, `IEEE TCAD`, `2025`, `CUHK`, `Interpretable`
