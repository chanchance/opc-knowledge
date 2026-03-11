# Optimizing Models Based OPC Fragmentation Using Genetic Algorithms

## 메타데이터
- **저자**: Domenico A. Dipaola, Ian Stobert
- **연도**: 2008
- **게재지**: Proc. SPIE 7122, Photomask Technology 2008, 71220V
- **DOI/URL**: https://doi.org/10.1117/12.801551
- **인용수**: ~25

## 핵심 요약
Model-based OPC(MBOPC)에서 가장 중요한 레시피 파라미터 중 하나인 단편화(fragmentation) 규칙을 유전 알고리즘(GA)으로 최적화하는 연구. GA를 이용해 단편화 파라미터를 조정하여 잔여 EPE를 최소화하면서 과도한 런타임이나 마스크 제조 문제를 방지한다. 어려운 금속 레이어 레이아웃 패턴을 대상으로 검증한다.

## 주요 기여
1. OPC 단편화 규칙을 GA로 체계적 최적화하는 방법론
2. EPE 최소화와 런타임/마스크 제조성의 균형 최적화
3. 금속 레이어 어려운 패턴에서의 단편화 규칙 검증
4. 마스크 데이터 보정 핵심 알고리즘이 아닌 파라미터 튜닝에 집중하는 실용적 접근

## Recipe/Process Flow 상세

### OPC 단편화 (Fragmentation) 개요
```
단편화 = 폴리곤 에지를 작은 세그먼트로 분할하는 과정

단편화 파라미터:
  uniform_seg: 균일 세그먼트 길이 (nm)
  min_seg: 최소 세그먼트 길이
  max_seg: 최대 세그먼트 길이
  corner_seg: 코너 주변 세그먼트 길이
  inner_corner: 내부 코너 처리 방식
  min_notch: 최소 노치 길이

단편화 영향:
  - 너무 거친 단편화: 낮은 DOF, 높은 EPE
  - 너무 세밀한 단편화: 높은 런타임, 마스크 복잡도 증가
  - 최적 단편화: 최소 EPE + 허용 런타임 + 마스크 제조 가능
```

### GA 기반 단편화 최적화
```
1. 최적화 공간 정의
   파라미터 벡터 θ = [uniform_seg, min_seg, corner_seg, ...]
   범위: 각 파라미터 [min, max] 설정

2. 적합도 함수
   F(θ) = w1 × RMS_EPE(θ) + w2 × max_EPE(θ)
          + w3 × Runtime_penalty(θ) + w4 × MRC_penalty(θ)

   여기서:
   - RMS_EPE: OPC 수렴 후 RMS edge placement error
   - max_EPE: 최대 EPE (핫스팟 방지)
   - Runtime_penalty: 세그먼트 수가 임계값 초과 시 페널티
   - MRC_penalty: 마스크 규칙 위반 세그먼트 수

3. GA 실행
   - 초기 집단: 현재 레시피 주변 랜덤 생성
   - 선택: 토너먼트 방식
   - 교배: 파라미터 단위 교환
   - 돌연변이: 범위 내 랜덤 변동

4. 검증
   - 최적 θ로 OPC 실행
   - 어려운 금속 패턴에서 EPE 감소 확인
   - 런타임 및 세그먼트 수 허용 범위 내 확인
```

### 금속 레이어 특수성
```
금속 레이어 어려운 패턴:
  - Dense metal lines (좁은 피치)
  - Metal end-of-line (line-end)
  - Metal-to-metal via interactions
  - Long wire segments with varying widths

단편화 최적화 효과:
  - EPE 감소: 특히 코너, 라인-엔드에서
  - Rippling 방지: 긴 와이어에서 균일한 보정
  - 런타임 제어: 불필요한 세밀 단편화 방지
```

### 성능 결과
```
최적화 전 (기본 규칙):
  RMS EPE: X nm
  런타임: T hours

최적화 후 (GA 최적 단편화):
  RMS EPE: 감소 (~20-30%)
  런타임: 허용 범위 유지
  마스크 제조: MRC 위반 없음
```

## OPC 툴 구현 관련성
- **SKOPC 단편화 엔진**: `skopc/modeling/model_opc.py`의 세그먼트 분할 파라미터를 YAML 레시피에서 GA로 최적화 가능
- **레시피 파라미터**: `uniform_seg`, `min_seg`, `corner_seg` 등을 SKOPC Recipe YAML의 표준 파라미터로 정의
- **2016년 논문과 상보**: Asthana(2016) 전체 OPC 레시피 GA vs. 본 논문 단편화 파라미터 전문 GA
- **MRC 통합**: `skopc/core/drc.py` MRC 체크를 단편화 최적화의 제약으로 통합

## 참고문헌
- Proc. SPIE 7122, Photomask Technology 2008
- 관련: OPC recipe optimization using genetic algorithm (SPIE 9780, 2016)
- 관련: Optimization of rule-based OPC fragmentation (SPIE 9661, 2015)
- 관련: Fast Forward OPC (SPIE 6730, 2007)

## 태그
`Recipe`, `SPIE`, `Fragmentation`, `GeneticAlgorithm`, `ModelBasedOPC`, `EdgeSegment`, `Runtime`, `MetalLayer`, `MRC`, `ParameterTuning`
