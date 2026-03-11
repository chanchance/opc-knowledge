# Large-Scale VLSI Mask Optimization: A Survey

## 메타데이터
- **저자**: Ziyang Yu, Bei Yu
- **연도**: 2025
- **게재지**: International Workshop on Advanced Patterning Solutions (IWAPS 2025), Shenzhen, China
- **DOI/URL**: https://www.cse.cuhk.edu.hk/~byu/papers/C280-IWAPS2025-OPC.pdf
- **인용수**: ~5

## 핵심 요약
전체 칩 규모 VLSI 마스크 최적화의 최신 발전을 체계적으로 조망하는 서베이 논문이다. 실용적 전체 칩 배치를 가능하게 하는 방법들에 초점을 맞추며, 물리 기반 솔버와 학습 기반 대리 모델을 포함한 가속 리소그래피 모델링, OPC/SRAF/ILT 마스크 최적화 기법, 그리고 확장 가능한 전체 칩 시스템 구현을 다룬다. CUHK Bei Yu 그룹의 광범위한 마스크 최적화 연구를 집약하는 키노트 서베이이다.

## 주요 기여
1. 전체 칩 규모 마스크 최적화 방법의 체계적 분류와 비교
2. 가속 리소그래피 모델링 (물리 기반 + 학습 기반 대리 모델)
3. OPC/SRAF/ILT 통합 관점에서의 최신 방법 비교
4. 전체 칩 배치를 위한 실용적 시스템 아키텍처 제시

## Recipe/Process Flow 상세

### 전체 칩 마스크 최적화의 과제
```
전체 칩 규모 (Full-Chip Scale):
  현대 IC 칩: 수억~수십억 트랜지스터
  레이아웃 면적: 수백 mm²
  마스크 클립 수: 수백만~수천만 클립

클립 단위 최적화의 한계:
  단순 합산: 클립당 1초 × 100M 클립 = 수년 소요
  타일 의존성: 인접 타일 광학 근접 효과 고려 필요
  경계 불일치: 타일 독립 최적화 → 스티칭 오류

전체 칩 최적화 전략:
  계층적 분할: 칩 → 블록 → 타일 → 클립
  병렬 처리: 다중 GPU, 분산 컴퓨팅
  경계 치유: 타일 경계 최적화 불일치 해결
```

### 가속 리소그래피 모델링 분류
```
물리 기반 가속:
  BRA (Better Approximation): Hopkins TCC 저랭크 분해
  SOCS (Sum of Coherent Sources): TCC 고유값 분해
  GPU FFT: CUDA 가속 항공 이미지 계산
  → 수십~수백 배 가속 (완전 시뮬 대비)

학습 기반 대리 모델:
  CNN 대리 모델: 레이아웃 → 이미지 직접 예측
  GAN 기반: 리소그래피 이미지 생성
  물리 내재 신경망: 물리 법칙 + 데이터 학습
  TorchLitho: 오픈소스 미분 가능 시뮬
  → ms 수준 예측 (물리 시뮬 대비 수천 배)

정확도-속도 트레이드오프:
  완전 시뮬: 높은 정확도, 느림
  BRA/SOCS: 높은 정확도, 중간 속도
  CNN 대리: 중간 정확도, 매우 빠름
  하이브리드: 패턴별 선택 적용
```

### OPC/SRAF/ILT 통합 분류
```
OPC 방법:
  Rule-based OPC (RB-OPC): 빠름, 낮은 정확도
  Model-based OPC (MB-OPC): 중간 속도, 높은 정확도
  AI-OPC: GNN, RL, DiffOPC → 빠름+높은 정확도
  ILT: 최고 정확도, 느림 → ML 가속 필요

SRAF 방법:
  Rule-based SRAF (RB-SRAF): 빠름, 복잡 패턴 한계
  CTM-SRAF: 연속 투과 마스크 기반 → 규칙 준수
  GAN-SRAF: 빠른 학습 기반 SRAF 생성
  RL-SRAF: 공정 윈도우 보상 직접 최적화
  LLM-SRAF: 프롬프트 기반 SRAF 생성

통합 접근:
  SMO (Source-Mask Optimization): 소스 + 마스크 동시
  NSGA-II SMO: 다목적 최적화 (DOF, EL 동시)
  RuleLearner: ILT → 규칙 자동 추출
```

### 전체 칩 시스템 아키텍처
```
산업 수준 전체 칩 ILT:
  분할: 계층적 타일 분할
  병렬: 다중 GPU 타일 동시 최적화
  치유: FuILT 경계 치유
  검증: 전체 칩 리소그래피 시뮬 검증

학술 연구 → 산업 격차:
  데이터셋: MaskOpt 등 공개 데이터셋
  벤치마크: ICCAD 2013, OpenILT
  실제 칩: 복잡한 2D 패턴, 다중 레이어
  MRC: 실제 마스크 설계 규칙 준수

미래 방향:
  LLM 통합: 프롬프트 기반 OPC/SRAF
  파운데이션 모델: 범용 마스크 최적화
  High-NA EUV: 새로운 M3D, 아나모픽 과제
  커비리니어 대중화: MBMW + DiffOPC
```

## OPC 툴 구현 관련성
- **SKOPC 로드맵**: 서베이의 전체 칩 시스템 아키텍처로 SKOPC 전체 칩 확장 설계
- **방법 선택**: 속도-정확도 트레이드오프 분석으로 SKOPC 백엔드 방법 선택
- **벤치마크**: MaskOpt, ICCAD 2013 기준으로 SKOPC 품질 평가
- **미래 기능**: LLM-SRAF, 파운데이션 모델 통합 계획에 활용

## 참고문헌
- IWAPS 2025, Shenzhen, China (October 2025)
- 저자 소속: CUHK (Ziyang Yu, Bei Yu)
- PDF: https://www.cse.cuhk.edu.hk/~byu/papers/C280-IWAPS2025-OPC.pdf
- 관련: 이 서베이가 다루는 모든 CUHK OPC/ILT/SRAF 연구들

## 태그
`Recipe`, `IWAPS`, `Survey`, `MaskOptimization`, `OPC`, `ILT`, `SRAF`, `FullChip`, `LargeScale`, `VLSI`, `CUHK`, `BeiYu`, `2025`
