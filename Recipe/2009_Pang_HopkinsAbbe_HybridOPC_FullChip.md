# Application of the Hybrid Hopkins-Abbe Method in Full-Chip OPC

## 메타데이터
- **저자**: Linyong Pang, Yong Liu, Douglas Abrams
- **연도**: 2009
- **게재지**: Microelectronic Engineering, Vol. 86, Issues 4-6 (also presented at SPIE/related conferences)
- **DOI/URL**: https://doi.org/10.1016/j.mee.2008.12.051
- **인용수**: ~40

## 핵심 요약
Hopkins 부분 가간섭 이미징 이론과 Abbe 이미징 이론의 장점을 결합한 하이브리드 Hopkins-Abbe(BRA) 방법을 풀칩 OPC에 적용하는 방법론을 제시한다. 표준 Hopkins 방법은 마스크 회절 효율이 상수라는 가정에 의존하여 고차 회절이 중요한 조건에서 오차가 발생하는데, BRA 방법은 이를 EM 산란 시뮬레이션으로 보완하면서 풀칩 속도를 유지한다. OPC 모델의 정확도와 계산 효율성을 동시에 향상시킨다.

## 주요 기여
1. Hopkins와 Abbe 방법의 한계 분석 및 하이브리드 BRA 방법 제안
2. 마스크 회절 계수의 비상수 특성을 EM 시뮬로 정확히 반영
3. 풀칩 OPC에 적용 가능한 계산 효율성 유지
4. 고차 회절이 중요한 복잡한 2D 패턴에서 정확도 향상

## Recipe/Process Flow 상세

### Hopkins vs. Abbe 이미징 이론
```
Abbe 이미징 (비간섭 합산):
  I(x) = Σ_s |Σ_n J_n T_n h(x, θ_s + nλ/p)|²
  - 각 조명 방향(s)에 대해 회절 이미지 독립 계산 후 합산
  - 장점: 직관적, 각 방향 기여 독립적 계산
  - 단점: 조명 방향 수에 비례하여 느림
  - 계산: O(N_source × N_pattern)

Hopkins 이미징 (TCF, 전달 상호 함수):
  I(x) = ΣΣ_mn TCC(m,n) d_m d_n* exp(i2π(m-n)x/p)
  TCC: 전달 상호 함수, 소스/광학계에만 의존
  d_m: m차 마스크 회절 계수
  - 장점: TCC 사전 계산 후 재사용, 빠름
  - 가정: d_m = 상수 (마스크 구조 무관)
  - 문제: 복잡한 2D 마스크에서 d_m이 변함 → 오차

하이브리드 BRA 방법:
  - 로컬 마스크 구조별 d_m을 EM 시뮬로 계산
  - EM 시뮬 결과로 TCC 보정
  - 복잡한 2D 패턴: EM 기여 → 정확도
  - 단순 1D 패턴: Hopkins 근사 → 속도
```

### OPC에서 BRA 방법 적용
```
OPC 모델 구성 요소:
  1. 광학 모델 (Hopkins TCC + BRA 보정)
     - 빠른 TCC 기반 기본 시뮬레이션
     - 2D 패턴 주변: BRA 보정 자동 활성화
     - 마스크 3D 효과: EM 산란 lookup 테이블

  2. 레지스트 모델 (컴팩트 모델)
     - CM1 또는 유사 파라미터화
     - 확산, 문턱값, 기울기 파라미터

OPC 이터레이션에서 BRA 활용:
  1D 세그먼트 (직선 구간): Hopkins TCC → 빠른 계산
  2D 세그먼트 (코너, 끝단): BRA → 정확한 계산
  혼합 전략: 계산 비용 최소화 + 정확도 유지

캘리브레이션:
  BRA 보정 파라미터 추출:
    EM 시뮬 기준 데이터 vs. Hopkins 단순 모델
    잔차 → BRA 보정항 피팅
```

### Hopkins vs. Abbe vs. BRA 비교
```
정확도 (2D 패턴 RMS EPE):
  Abbe: 높은 정확도 (기준)
  Hopkins: 1D 패턴 동등, 2D 패턴 오차
  BRA: Abbe에 근접한 정확도, Hopkins보다 우수

계산 속도 (풀칩 OPC):
  Abbe: 느림 (조명 방향 수 × 패턴 수)
  Hopkins: 빠름 (TCC 재사용)
  BRA: Hopkins에 근접한 속도 (BRA 보정은 로컬)

결론:
  풀칩 OPC에서 BRA가 정확도/속도 최적 균형
  특히 193nm 이후 노드에서 2D 패턴 비율 증가 → BRA 중요성 증가
```

### 풀칩 적용 결과
```
65nm 이하 노드 OPC 검증:
  BRA 모델: 복잡한 2D 패턴 정확도 향상
  런타임 오버헤드: 허용 가능한 수준

마스크 3D 효과 통합:
  BRA 방법의 EM 시뮬 컴포넌트에 마스크 3D 효과 자연스럽게 통합
  별도 M3D 보정 불필요 (일부 효과 자동 포함)
```

## OPC 툴 구현 관련성
- **SKOPC 광학 모델**: `skopc/core/litho_engine.py`에 Hopkins TCC + BRA 보정 구조 도입
- **1D/2D 자동 선택**: 세그먼트 분류 후 1D는 Hopkins, 2D는 BRA 자동 라우팅
- **TCC 캐싱**: 조명/광학 파라미터 고정 시 TCC 미리 계산 후 캐시
- **EM 룩업 테이블**: 복잡한 마스크 구조의 EM 시뮬 결과를 테이블로 저장/검색

## 참고문헌
- Microelectronic Engineering, Vol. 86 (2009)
- 저자 소속: Luminescent Technologies
- 관련: Hopkins versus Abbe: a lithography simulation matching study (SPIE 4691, 2002)
- 관련: Toward standard process models for OPC (SPIE 6520, 2007)
- 관련: Advanced OPC Mask-3D and Resist-3D modeling (SPIE 9052, 2014)

## 태그
`Recipe`, `OPC-Modeling`, `Hopkins`, `Abbe`, `HybridModel`, `PartialCoherence`, `TCC`, `EM-Simulation`, `FullChip`, `2D-Pattern`, `2009`
