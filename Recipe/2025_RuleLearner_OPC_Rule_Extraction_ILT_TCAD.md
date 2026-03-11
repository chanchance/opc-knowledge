# RuleLearner: OPC Rule Extraction From Inverse Lithography Technique Engine

## 메타데이터
- **저자**: Ziyang Yu, Su Zheng, Wenqian Zhao, Shuo Yin, Guojin Chen, Bei Yu, Martin D. F. Wong
- **연도**: 2025
- **게재지**: IEEE Transactions on Computer-Aided Design (TCAD), Vol. 44, No. 5, May 2025
- **DOI/URL**: https://ieeexplore.ieee.org/document/10753456
- **인용수**: ~5

## 핵심 요약
ILT(Inverse Lithography Technology) 엔진의 결과에서 OPC 규칙(rule)을 자동 추출하는 RuleLearner 프레임워크를 제안한다. SRAF 삽입 규칙(SRAF 크기/거리 테이블)과 Model-based OPC 규칙을 ILT 결과에서 학습하며, 규칙 값 분포를 자연 기울기(natural gradient)로 최적화하여 실제 산업 시나리오에서도 우수한 리소그래피 성능과 계산 효율성을 달성한다.

## 주요 기여
1. ILT 엔진 결과에서 SRAF 규칙 + OPC 규칙 자동 추출
2. 정보 증강(information-augmented) ILT 엔진으로 규칙 학습 지도
3. 자연 기울기(natural gradient) 기반 규칙 값 분포 최적화
4. 복잡한 2D 패턴과 다양한 설계에서 최고 리소그래피 성능 + 계산 효율

## Recipe/Process Flow 상세

### 규칙 기반 OPC와 ILT의 트레이드오프
```
규칙 기반 OPC (RB-OPC):
  SRAF 규칙: Space-Width 테이블 → 크기/위치 결정
  OPC 규칙: CD/pitch별 바이어스 테이블
  장점: 빠름, 결정론적, 검증 용이
  단점:
    전문가 설계 규칙: 시간 소모, 노드 전환 시 재작성
    복잡한 2D 패턴: 규칙 테이블 적용 한계

ILT (Inverse Lithography):
  규칙 없는 수치 최적화 → 최고 리소그래피 성능
  장점: 패턴별 최적 마스크, SRAF 자동 생성
  단점: 느림 (전체 칩: 수십 시간), 결과 불일관성

RuleLearner 목표:
  ILT 결과에서 규칙 자동 학습
  → 규칙 기반의 속도 + ILT 수준 품질
  → 전문가 없이 신규 노드 규칙 자동 생성
```

### 정보 증강 ILT 엔진
```
표준 ILT:
  최적화: min_M L_litho(M, target)
  결과: 최적 마스크 M* (규칙 정보 없음)

정보 증강 ILT:
  규칙 파라미터 θ = {SRAF_size, SRAF_dist, OPC_bias, ...}를 명시적으로 표현
  최적화: min_θ L_litho(M(θ), target)
  M(θ): θ에 의해 파라미터화된 마스크 생성 규칙
  결과: 최적 규칙 파라미터 θ*

규칙 파라미터 그룹:
  SRAF 관련:
    d_sraf: SRAF-주 패턴 간 거리
    w_sraf: SRAF 폭
    n_sraf: SRAF 수 (1, 2, 3행)
  OPC 관련:
    bias_line: 라인 CD 바이어스
    bias_corner: 코너 OPC 바이어스
    bias_end: 라인 끝단 바이어스
```

### 자연 기울기 최적화
```
문제: 규칙 값 분포 최적화의 비선형성
  로컬 OPC 성능 vs. 글로벌 일관성 트레이드오프
  단순 기울기 하강: 로컬 최적에 갇히는 경향

자연 기울기 (Natural Gradient):
  피셔 정보 행렬(Fisher Information Matrix) 활용
  g_nat = F^(-1) × g_euclidean
  효과: 규칙 파라미터 분포 공간에서 최적 이동 방향
  장점:
    로컬 패턴 성능 + 글로벌 일관성 균형
    비선형 분포에서 더 빠른 수렴
    SRAF 규칙 테이블의 단조성(monotonicity) 유지

구현:
  다양한 패턴 유형에서 ILT 실행 → θ* 수집
  자연 기울기로 규칙 값 분포 최적화
  최종: OPC 규칙 테이블 자동 생성
```

### 전체 흐름
```
1단계: 훈련 패턴 수집
  다양한 CD/pitch/density 패턴 라이브러리

2단계: 정보 증강 ILT 실행
  각 패턴 → 규칙 파라미터 θ* 추출

3단계: 규칙 분포 학습
  θ* 데이터 → 자연 기울기 최적화
  → 규칙 값 분포 P(θ | 패턴 특성)

4단계: 규칙 테이블 생성
  P(θ | CD, pitch, density) → 이산화 → 룩업 테이블
  SRAF 규칙 테이블: (Space, Width) → (d_sraf, w_sraf)
  OPC 규칙 테이블: (CD, pitch) → bias

5단계: 적용
  새 레이아웃 → 규칙 테이블 룩업 → SRAF 삽입 + OPC
  속도: Rule-based 수준, 품질: ILT 근접
```

### 성능 결과
```
리소그래피 성능 (EPE, 공정 윈도우):
  RuleLearner: 기존 RB-SRAF/RB-OPC 대비 우수
  RuleLearner: ILT와 근접 또는 동등

계산 효율:
  ILT 대비: 규칙 적용 단계 수백 배 빠름
  전체 칩 적용: ILT 대비 실용적 TAT

다양한 패턴 일반화:
  복잡한 2D 패턴: 규칙 학습 성공
  다양한 레이어: 노드별 자동 규칙 생성
```

## OPC 툴 구현 관련성
- **SKOPC 규칙 추출**: ILT 결과에서 SKOPC 규칙 테이블 자동 생성 파이프라인
- **SRAF 규칙 테이블**: `skopc/modeling/sraf_generator.py`에 RuleLearner 추출 규칙 통합
- **OPC 규칙 캘리브레이션**: 신규 공정 노드 전환 시 ILT → 자동 규칙 추출
- **자연 기울기**: 규칙 분포 최적화에 Fisher 정보 행렬 활용

## 참고문헌
- IEEE TCAD, Vol. 44, No. 5, May 2025
- 저자 소속: CUHK (Bei Yu, Martin Wong 그룹)
- 관련: L2O-ILT (TCAD 2024)
- 관련: Neural-ILT (ICCAD 2020 / TCAD 2022)
- 관련: DevelSet (ICCAD 2021 / TCAD 2023)
- 관련: CTM-SRAF (TCAD 2023)

## 태그
`Recipe`, `IEEE`, `TCAD`, `OPC`, `RuleExtraction`, `ILT`, `SRAF`, `NaturalGradient`, `RuleBasedOPC`, `AutomatedRule`, `CUHK`, `BeiYu`, `2025`
