# Multiple-Step Process Window Aware OPC for Hyper-NA Lithography

## 메타데이터
- **저자**: C.T. Hsuan, C.M. Hu, Fred Lo, Elvis Yang, T.H. Yang, K.C. Chen, Chih-Yuan Lu
- **연도**: 2013
- **게재지**: Proc. SPIE 8683, Optical Microlithography XXVI, 868323
- **DOI/URL**: https://doi.org/10.1117/12.2011061
- **인용수**: ~25

## 핵심 요약
기존 PWOPC(Process Window OPC)는 최악 핫스팟의 CD 변동을 줄이지만 과보상으로 새로운 약점을 발생시킬 수 있다. 본 논문은 43nm 반피치 다마신(damascene) 금속 레이어에서 핫스팟을 레이아웃에서 분리하여 다양한 핫스팟 유형에 서로 다른 CD 허용 오차를 적용하는 다단계 공정 윈도우 인식 OPC 방법론을 제안한다.

## 주요 기여
1. 핫스팟 격리 기반 다단계 PWOPC: 핫스팟 유형별 독립적 CD 허용 오차 설정
2. 과보상으로 인한 신규 약점 발생 방지
3. 43nm 다마신 금속 레이어에서 모든 핫스팟의 공정 윈도우 유지
4. 기존 PWOPC 대비 개선된 전체 칩 공정 강건성

## Recipe/Process Flow 상세

### 기존 PWOPC의 문제점
```
기존 PWOPC 흐름:
  전체 칩 → 단일 PWOPC 파라미터 → 수렴

  문제:
  - 가장 나쁜 핫스팟을 기준으로 OPC 설정
  - 일부 패턴에서 과보상(over-correction) 발생
  - 과보상 → 인접 패턴에 새로운 핫스팟 생성
  - 요구사항이 다른 핫스팟 간 충돌
```

### 다단계 PWOPC 알고리즘
```
1단계: 핫스팟 식별 및 분류
────────────────────────────
a) 초기 OPC 실행 (표준 OPC)
b) 전체 칩 공정 윈도우 평가
c) 핫스팟 식별: PV 밴드 기준 미달 영역
d) 핫스팟 분류:
   Type A: 밀집(dense) 패턴 핫스팟 → 좁은 DOF 요구
   Type B: 고립(isolated) 패턴 핫스팟 → 다른 OPC 요구
   Type C: 2D 구조 핫스팟 → 특수 처리 필요

2단계: 핫스팟 격리
────────────────────
a) 각 핫스팟 유형을 레이아웃에서 분리
b) 각 유형별 독립적 CD 허용 오차 설정
   Type A: ΔCD_A (좁은 허용 범위)
   Type B: ΔCD_B (다른 허용 범위)
   Type C: ΔCD_C (특화된 허용 범위)
c) 유형 간 충돌 방지 규칙 적용

3단계: 유형별 독립적 PWOPC
────────────────────────────
For each hotspot type T:
  a) 해당 유형 패턴에만 PWOPC 적용
     목적함수: 공정 윈도우 (F, D) 조건에서 ΔCD < ΔCD_T
  b) 이터레이션: PWOPC 수렴
  c) 비핫스팟 영역: 표준 OPC 또는 완화된 기준 적용

4단계: 통합 및 검증
────────────────────
a) 각 유형 OPC 결과 통합
b) 전체 칩 공정 윈도우 재평가
c) 신규 핫스팟 발생 확인
d) 필요시 추가 이터레이션
```

### 다마신 금속 레이어 특수성
```
다마신 구조: 금속선을 트렌치에 매립하는 방식
특수 고려사항:
  - 금속 밀도 변화로 인한 CMP 효과
  - Via-to-metal 정렬 요구
  - Hyper-NA (NA > 1.0) 액침 리소그래피 사용

43nm 반피치:
  k1 < 0.3 (극저 k1)
  강한 근접 효과
  핫스팟 집중 발생
```

### 성능 결과
```
기존 PWOPC:
  최악 핫스팟 개선 ○
  신규 약점 발생 ○ (문제)

다단계 PWOPC:
  모든 핫스팟 동시 유지 ○
  신규 약점 없음 ○
  전체 칩 PV 밴드 개선
```

## OPC 툴 구현 관련성
- **SKOPC PWO 모듈**: `skopc/pwo/` NSGA-II 기반 공정 윈도우 최적화에 핫스팟 분류별 다단계 전략 적용 가능
- **핫스팟 격리**: `skopc/recipe/` 배치 실행기에서 핫스팟 레이어를 분리하여 독립 OPC 실행
- **CD 허용 오차 파라미터**: 핫스팟 유형별 ΔCD를 SKOPC YAML 레시피에 레이어/패턴 유형별로 정의
- **TSMC 출처**: TSMC 연구팀의 첨단 노드 양산 OPC 전략

## 참고문헌
- Proc. SPIE 8683, Optical Microlithography XXVI (2013)
- 저자 소속: TSMC (Taiwan Semiconductor Manufacturing Company)
- 관련: Process variation aware OPC with VLIM (DAC, 2006)
- 관련: Full chip process window OPC based on matrix retargeting (SPIE, 2016)

## 태그
`Recipe`, `SPIE`, `ProcessWindowOPC`, `PWOPC`, `HotspotIsolation`, `MultistepOPC`, `HyperNA`, `DamasceneMetal`, `TSMC`, `43nm`
