# Automatic OPC Repair Flow: Optimized Implementation of the Repair Recipe

## 메타데이터
- **저자**: Mohamed Bahnas, Mohamed Al-Imam, James Word
- **연도**: 2007
- **게재지**: Proc. SPIE 6730, Photomask Technology 2007, 67303S
- **DOI/URL**: https://doi.org/10.1117/12.746950
- **인용수**: ~20

## 핵심 요약
OPC 흐름에서 발생한 위반(violation)을 자동으로 수정하는 OPC 수리 흐름(repair flow)의 최적 구현 방법론을 제시한다. OPC 완료 후 검증(LRC/ORC) 단계에서 발견된 핫스팟(EPE 초과, 브릿지/핀치 위험)을 수작업 없이 자동으로 보정하는 수리 레시피(repair recipe) 설계와 그 최적화 전략을 다룬다. 수리 흐름을 표준 OPC 레시피 내에 통합하여 효율성을 높이는 방안을 제시한다.

## 주요 기여
1. OPC 검증 후 자동 수리 흐름 아키텍처 및 레시피 설계
2. 수리 레시피의 파라미터 최적화 방법론
3. 수리 흐름의 표준 OPC 레시피 통합 전략
4. 수리 후 검증 루프를 포함한 완성된 OPC-수리-검증 사이클

## Recipe/Process Flow 상세

### OPC 수리 흐름의 필요성
```
표준 OPC 흐름:
  설계 → OPC → 검증(LRC/ORC) → 테이프아웃

  문제:
  OPC 후 검증에서 위반 발견:
    EPE 초과 세그먼트
    브릿지(Bridge) 위험 패턴
    핀치(Pinch) 위험 패턴
    공정 윈도우 기준 미달 패턴

기존 수리 방법:
  수작업: 엔지니어가 핫스팟 개별 수정
    → 시간 소모 (수일~수주)
    → 일관성 없음
    → 새로운 핫스팟 유발 가능

자동 수리 흐름:
  핫스팟 → 수리 레시피 자동 적용 → 재검증
  → 수작업 없이 반복 가능
  → 일관적 수리 결과
  → 빠른 TAT
```

### 자동 OPC 수리 흐름 아키텍처
```
수리 흐름 단계:

1단계: 핫스팟 식별 및 분류
  LRC 결과에서 위반 목록 추출:
    타입 A: EPE 초과 (허용 오차 이상 CD 오차)
    타입 B: 브릿지 위험 (두 패턴 간 간격 부족)
    타입 C: 핀치 위험 (패턴 너무 좁아짐)
    타입 D: 공정 윈도우 기준 미달

2단계: 수리 영역 정의
  각 핫스팟 주변의 수리 윈도우(repair window) 정의
  영향 반경 고려: 수리 영향이 미치는 최대 거리
  충돌 방지: 인접 수리 영역 간 우선순위 결정

3단계: 수리 레시피 적용
  타입별 수리 전략:
    EPE 초과: 해당 세그먼트 재이동 (강화된 OPC)
    브릿지: 두 패턴 간 격리 마진 강화 (축소 방향 OPC)
    핀치: 패턴 폭 확대 (확대 방향 OPC)
    공정 윈도우: 인접 SRAF 추가 또는 크기 조정

4단계: 수리 후 재검증
  수리된 영역에서 LRC 재실행
  개선 여부 확인:
    개선됨 → 수리 완료
    미개선 → 수리 파라미터 조정 후 재시도
    악화됨 → 수리 롤백, 다른 전략 시도

5단계: 전체 칩 재검증
  수리 영향이 주변에 미쳤는지 확인
  새로운 위반 발생 여부 검사
```

### 수리 레시피 파라미터 최적화
```
수리 레시피 핵심 파라미터:

  1. 수리 윈도우 크기:
     너무 작음: 수리 자유도 제한 → 효과 미흡
     너무 큼: 광범위 변경 → 새로운 위반 유발
     최적: 핫스팟 유형 및 심각도에 따라 동적 설정

  2. 수리 이터레이션 수:
     적음: 미수렴 → 핫스팟 잔존
     많음: 런타임 증가
     최적: 위반 강도에 비례하여 설정

  3. 수리 레시피 파라미터 (OPC 파라미터 대비):
     더 작은 스텝 크기: 인접 패턴 영향 최소화
     강화된 시뮬레이션 정확도: 핫스팟 주변 엄밀 모델

  4. 수리 우선순위:
     심각도 높은 핫스팟 먼저 수리
     상호 영향 패턴 그룹 처리
```

### 표준 OPC 레시피 통합
```
통합 방법:
  Option 1: 순차적 실행
    표준 OPC → 검증 → 수리 OPC → 검증 (루프)
    장점: 단순한 흐름
    단점: 두 번의 OPC 실행으로 런타임 증가

  Option 2: OPC 레시피 내 통합
    OPC 레시피에 수리 단계 내장
    OPC 이터레이션 완료 후 핫스팟 검사 및 국소 수리
    장점: 단일 OPC 실행으로 수리 포함
    단점: 레시피 복잡도 증가

권장: Option 2
  OPC 레시피 구조:
    [일반 OPC 단계] → [핫스팟 식별] → [수리 단계] → [검증]
  파라미터:
    repair_enabled: true/false
    repair_max_iterations: 수리 최대 이터레이션
    repair_window_size: μm 단위 수리 영역 크기
    repair_violation_types: [bridge, pinch, epe]
```

### 성능 결과
```
수작업 수리 대비 자동 수리:
  수리 시간: 수일 → 수시간 (>10× 단축)
  수리 일관성: 개선 (자동화로 인적 오류 제거)
  새로운 위반 유발: 감소

핫스팟 해결률:
  자동 수리로 대부분(>90%) 핫스팟 해결 가능
  잔존 핫스팟: 수작업 수정 또는 설계 변경 필요
```

## OPC 툴 구현 관련성
- **SKOPC 수리 흐름**: `skopc/recipe/` 배치 러너에 repair_flow 단계 추가
- **핫스팟 분류**: LRC 결과를 bridge/pinch/epe 타입으로 분류하는 파서
- **수리 레시피 YAML**: OPC 레시피의 repair 섹션에 수리 파라미터 정의
- **재검증 루프**: 수리 후 자동 재검증 → 새로운 위반 확인 → 반복 루프 구현

## 참고문헌
- Proc. SPIE 6730, Photomask Technology 2007
- 관련: Automatic OPC mask shape repair (SPIE 6521, 2007)
- 관련: Metal layer OPC repair flow for 28nm (IEEE, 2016)
- 관련: Fast OPC repair flow based on machine learning (SPIE 11328, 2020)

## 태그
`Recipe`, `SPIE`, `OPC-RepairFlow`, `AutomaticRepair`, `LRC`, `HotspotRepair`, `Bridge`, `Pinch`, `RepairRecipe`, `OPC-Verification`, `2007`
