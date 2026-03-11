# Process-Variation-Aware Rule-Based Optical Proximity Correction for Analog Layout Migration

## 메타데이터
- **저자**: (IEEE document 7738428 - IEEE Transactions 2016)
- **연도**: 2016
- **게재지**: IEEE Journals & Magazine (IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems 추정)
- **DOI/URL**: https://ieeexplore.ieee.org/document/7738428
- **인용수**: ~40

## 핵심 요약
아날로그 레이아웃의 고유한 특성을 활용한 공정 변동 인식 Rule-Based OPC(RB-OPC) 방법론을 아날로그 레이아웃 마이그레이션 공정에 통합한다. RB-OPC의 정확도 한계를 국소 와이어 폭 확장(wire widening)과 와이어 이동(wire shifting) 연산으로 보완하며, PV-밴드 시프팅으로 아날로그 회로 성능을 공정 변동으로부터 보호한다. 상용 및 학술 디지털 솔루션 대비 높은 효율성, 낮은 마스크 복잡도, 허용 가능한 EPE를 달성한다.

## 주요 기여
1. 아날로그 레이아웃 마이그레이션에 통합된 PV 인식 RB-OPC 방법론
2. 와이어 폭 확장/이동으로 RB-OPC 정확도 한계 보상
3. PV-밴드 시프팅으로 공정 변동 하에서 아날로그 회로 매칭 블록 성능 보존
4. 아날로그 회로의 OPC 연구 공백을 최초로 체계적으로 다룸

## Recipe/Process Flow 상세

### 아날로그 레이아웃 OPC의 특수성
```
디지털 OPC와의 차이:
  디지털: 기능적 정확성 → EPE 최소화로 충분
  아날로그: 소자 매칭(matching), 기생 성분, 대칭성이 핵심

아날로그 OPC 요구사항:
  - 매칭 블록(matching block) 내 균일한 CD
  - 공정 변동 하에서도 회로 성능 유지
  - 낮은 마스크 복잡도 (아날로그 레이아웃의 특성상)
```

### PV 인식 RB-OPC + 와이어 연산 알고리즘
```
1. 공정 변동 모델링
   - 리소그래피 공정 변동 시뮬레이션 (focus, dose)
   - 각 공정 조건에서의 CD 예측
   - PV-밴드: 모든 조건에서의 CD 범위

2. Rule-Based OPC 적용
   - Space-Width 테이블로 표준 RB-OPC 보정
   - 아날로그 레이아웃의 상대적으로 단순한 기하구조 활용
   - 빠른 실행 속도

3. 국소 와이어 연산으로 정확도 보완
   a) 와이어 폭 확장 (Wire Widening):
      - RB-OPC 한계로 EPE 초과 시 와이어 폭 조정
      - 좁은 금속선: 폭 확장으로 공정 윈도우 개선

   b) 와이어 이동 (Wire Shifting):
      - 비대칭 근접 효과 보상
      - 와이어를 목표 위치로 이동

4. PV-밴드 시프팅 (Analog 특화)
   - 매칭 블록 내 소자들의 PV 밴드 정렬
   - PV 밴드를 동일한 방향으로 시프팅
   - 공정 변동 하에서도 소자 간 매칭 유지
   - 아날로그 회로 성능 보호 (Vt, Ion 매칭)
```

### PV-밴드 시프팅 상세
```
아날로그 매칭 블록:
  소자 M1, M2 (매칭 쌍)

문제: M1과 M2의 PV 밴드가 서로 다른 방향으로 시프트
  → 공정 변동 하에서 M1 ≠ M2

PV-밴드 시프팅 해결:
  M1의 OPC를 M2와 동일한 PV 밴드 방향이 되도록 조정
  → 공정 변동 후에도 M1 ≈ M2 (매칭 유지)

수식:
  ΔCD_M1(ΔF, ΔD) ≈ ΔCD_M2(ΔF, ΔD)  ∀(ΔF, ΔD) ∈ PW
```

### 성능 결과 (상용 디지털 솔루션 대비)
```
효율성: 높음 (RB-OPC + 와이어 연산의 낮은 런타임)
마스크 복잡도: 낮음 (RB-OPC 단순성)
EPE: 허용 가능 범위
아날로그 매칭: PV-밴드 시프팅으로 보존
```

## OPC 툴 구현 관련성
- **SKOPC 아날로그 레이어 지원**: `skopc/modeling/`에 아날로그 레이아웃 전용 OPC 모드 추가 참조
- **RB-OPC 기반**: `skopc/modeling/rule_opc.py`의 Rule-based OPC에 PV 인식 기능 통합 가능
- **매칭 블록 처리**: 아날로그 회로 매칭 블록 식별 및 PV-밴드 동기화 처리
- **SKOPC Recipe**: 아날로그 레이어에 대한 별도 OPC 레시피 파라미터 정의

## 참고문헌
- IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (2016), Document 7738428
- 관련: Analog layout retargeting with PV-aware RB-OPC (IEEE, 2017)
- 관련: Process variation aware OPC with VLIM (DAC, 2006)
- 관련: Classical control theory applied to OPC convergence (SPIE, 2004)

## 태그
`Recipe`, `IEEE`, `RuleBasedOPC`, `AnalogLayout`, `ProcessVariation`, `PVBand`, `WireWidening`, `MatchingBlock`, `LayoutMigration`, `2016`
