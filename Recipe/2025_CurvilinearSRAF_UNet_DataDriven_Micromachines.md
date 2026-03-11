# Curvilinear Sub-Resolution Assist Feature Placement Through a Data-Driven U-Net Model

## 메타데이터
- **저자**: (MDPI Micromachines, 2025)
- **연도**: 2025
- **게재지**: MDPI Micromachines, Vol. 16, No. 11, Article 1229 (October 2025)
- **DOI/URL**: https://www.mdpi.com/2072-666X/16/11/1229
- **인용수**: ~5

## 핵심 요약
커비리니어(곡선형) 서브해상도 보조 피처(SRAF) 배치를 위한 데이터 기반 U-Net 모델을 제안한다. 기존 SRAF 배치 방법론이 속도와 패턴 충실도 사이의 트레이드오프 문제를 가지며 첨단 노드에 필수적인 커비리니어 레이아웃 최적화에 실패하는 문제를 해결한다. 레벨셋 방법(LSM)으로 생성한 최적 커비리니어 SRAF를 학습 레이블로 활용하여 대규모 데이터셋을 구축하고, U-Net이 CPU 기반 방법 대비 수 오더 크기의 가속을 달성하면서 LSM과 유사한 광학 성능을 제공한다.

## 주요 기여
1. 커비리니어 SRAF 배치를 위한 최초의 데이터 기반 U-Net 모델
2. 레벨셋 방법(LSM) 결과를 학습 레이블로 활용한 대규모 데이터셋 구축
3. CPU 기반 대비 수 오더 크기 가속, GPU 가속 알고리즘 대비도 유의미한 향상
4. LSM과 비슷한 광학 성능 (PVB, EPE) 달성

## Recipe/Process Flow 상세

### 커비리니어 SRAF의 필요성
```
기존 직교형 SRAF 한계:
  Rule-based SRAF: 직사각형 형상, 빠름
    → 복잡한 2D 패턴에서 최적 성능 미달
  Model-based SRAF: 직교형 최적화, 정확
    → 커비리니어 형상 생성 불가
  ILT 기반 SRAF: 최고 성능, 매우 느림
    → 전체 칩 적용 불가

커비리니어 SRAF 장점:
  자유 형상: 주 피처 주변 최적 광학 근접 보정
  공정 윈도우: PVB 최소화, DOF 확장
  EUV/ArF 193i: 고급 노드 프린팅 향상
  마스크 제조: MBMW (멀티빔 마스크 라이터)로 제조 가능
```

### 데이터셋 구축
```
입력 데이터:
  소스: 다양한 반도체 레이아웃 패턴
  전처리: 주 피처 레이아웃 → 이진 이미지
  크기: 512×512 픽셀 타일 (일반적)

Ground Truth 생성 (레벨셋 방법):
  Level-Set Method (LSM):
    - 레벨셋 함수로 SRAF 경계 표현
    - 광학 성능만을 위한 순수 최적화
    - 출력: 최적 커비리니어 SRAF 형상
  레이블: 이진 커비리니어 SRAF 마스크 이미지

대규모 구성:
  다양한 패턴 유형: 1D 라인/공간, 2D 복잡 패턴
  다양한 피치/CD: 첨단 노드 범위 포괄
  MRC 처리: LSM 결과에 광학 최적화 우선 (MRC 후처리)
```

### U-Net 아키텍처
```
인코더-디코더 구조:
  인코더:
    - Conv + BN + ReLU 블록 반복
    - MaxPooling: 공간 해상도 감소
    - 깊어질수록 채널 증가 (64→128→256→512)

  병목 레이어:
    - 가장 높은 추상화 레벨
    - 전역 패턴 정보 인코딩

  디코더:
    - 전치 컨볼루션: 업샘플링
    - 스킵 연결: 인코더 특징 직접 연결
    - 세부 경계 정보 복원

  출력:
    - 커비리니어 SRAF 확률 맵 (0~1)
    - 이진화: 임계값 → 최종 SRAF 마스크

손실 함수:
  L_total = L_BCE + w_PVB × L_PVB + w_EPE × L_EPE
  L_BCE: 픽셀 단위 이진 교차 엔트로피 (형상 유사도)
  L_PVB: PV 밴드 손실 (광학 성능)
  L_EPE: EPE 손실 (엣지 정확도)
```

### 성능 결과
```
속도:
  CPU LSM 대비: 수 오더 크기(~100~1000×) 가속
  GPU 가속 알고리즘 대비: 유의미한 추가 가속
  → 전체 칩 실용적 런타임 달성

광학 성능:
  PVB: LSM 결과와 매우 유사 (비교 가능한 공정 윈도우)
  EPE: LSM 생성 SRAF와 높은 패턴 충실도
  U-Net 생성 SRAF: 고품질 커비리니어 형상 유지

비교:
  Rule-based SRAF 대비: 유의미한 PVB 개선
  직교형 MB-SRAF 대비: 커비리니어의 추가 이점
```

### 미래 방향
```
통합 최적화:
  SRAF + OPC 동시 최적화 U-Net 확장
  MRC 인식 커비리니어 SRAF (MRC 제약 포함)

일반화:
  다양한 공정 노드 적응
  전이 학습으로 새 노드 빠른 적응
  파운데이션 모델: 범용 SRAF 생성기
```

## OPC 툴 구현 관련성
- **SKOPC 커비리니어 SRAF**: U-Net 아키텍처로 SKOPC SRAF 생성기에 커비리니어 지원 추가
- **데이터 파이프라인**: LSM 기반 학습 데이터 생성 → SKOPC U-Net SRAF 훈련
- **MaskOpt 통합**: 커비리니어 SRAF U-Net + MBMW 마스크 데이터 준비 파이프라인
- **속도 목표**: CPU LSM 대비 수 오더 가속으로 실시간 SRAF 배치 달성

## 참고문헌
- MDPI Micromachines, Vol. 16, No. 11, Article 1229 (October 2025)
- DOI: https://doi.org/10.3390/mi16111229
- PMC: https://pmc.ncbi.nlm.nih.gov/articles/PMC12654570/
- 관련: CTM-SRAF (IEEE TCAD 2023)
- 관련: LLM-SRAF (DATE 2025)
- 관련: RL-SRAF + Transfer Learning (ICCAD 2022)

## 태그
`Recipe`, `Micromachines`, `MDPI`, `SRAF`, `Curvilinear`, `UNet`, `DeepLearning`, `DataDriven`, `LevelSet`, `ProcessWindow`, `PVBand`, `MaskSynthesis`, `2025`
