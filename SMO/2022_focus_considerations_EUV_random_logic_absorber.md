# Focus Considerations of Design Pitches and Absorber Choice for EUV Random Logic

## 메타데이터
- **저자**: (SPIE 12051 저자 정보)
- **연도**: 2022
- **게재지**: Proc. SPIE 12051, Optical Microlithography XXXV, 2614296 (2022)
- **DOI/URL**: https://doi.org/10.1117/12.2614296

## 핵심 요약
EUV 랜덤 로직 패터닝에서 설계 피치와 흡수층 선택이 포커스(초점) 특성에 미치는 영향을 분석한다. TaBN을 기준으로 다양한 흡수층 재료에 대한 베스트 포커스(BF)와 초점 심도(DOF)를 시뮬레이션으로 분석하여, 랜덤 로직 레이아웃의 다양한 피치에 걸쳐 최적 포커스 조건을 제시한다.

## 주요 기여
1. **흡수층별 BF/DOF 분석**: TaBN, low-n 등 흡수층 재료가 베스트 포커스와 DOF에 미치는 영향
2. **피치 의존 포커스 특성**: 랜덤 로직의 다양한 피치에서 포커스 조건 변화 분석
3. **through-pitch 포커스 균일화**: 모든 피치에서 포커스 조건을 균일화하는 흡수층/소스 선택
4. **SMO와 흡수층 선택 연계**: 포커스 특성을 고려한 최적 흡수층 선택 기준 제시

## 알고리즘/수식
### 흡수층 포커스 특성 분석
```
베스트 포커스 이동 (BFS):
  BFS(pitch, material) = f(n, k, t_abs, pitch, NA)
  TaBN: BFS_ref(pitch)
  Low-n: BFS_low-n(pitch) ≠ BFS_ref(pitch)

DOF 비교:
  DOF(pitch, material) = 2 × |Δfocus| where CD ≤ CD_spec

Through-pitch 포커스 균일성:
  Δ BFS = max_{pitch} BFS(pitch) - min_{pitch} BFS(pitch)
  목표: Δ BFS 최소화 → 모든 피치에서 동일 포커스 설정

SMO와 결합:
  소스 형상 최적화로 BFS(pitch) 의존성 완화 가능
  → SMO + 흡수층 선택 공동 최적화
```

### 랜덤 로직 피치 분포
```
랜덤 로직 피치 범위:
  금속 레이어: 24nm ~ 80nm (다양한 피치 공존)
  비아 레이어: 단일 피치 근방

포커스 설정:
  스캐너는 단일 포커스 오프셋 설정
  → 모든 피치에서 최적 포커스 달성 어려움
  → 흡수층 선택으로 BFS 분산 최소화 필요
```

## OPC 툴 SMO 구현 관련성
- 포커스 인식 SMO: BFS(pitch) 분산을 SMO 비용 함수에 포함
- 흡수층 선택 가이드: 랜덤 로직 레이아웃에 최적 흡수층 추천 기준
- Through-pitch OPC: 피치별 BFS 차이를 OPC 마스크 바이어스에 반영
- SKOPC SMO 모듈: 포커스 균일성 항을 SMO 비용 함수에 추가

## 태그
`EUV`, `BFS`, `DOF`, `absorber`, `TaBN`, `low_n`, `random_logic`, `through_pitch`, `focus`, `SMO`, `OPC`, `SPIE`, `2022`
