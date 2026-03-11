# MaskOpt: A Large-Scale Mask Optimization Dataset to Advance AI in Integrated Circuit Manufacturing

## 메타데이터
- **저자**: (arXiv:2512.20655 - 2025)
- **연도**: 2025
- **게재지**: arXiv:2512.20655 (December 2024; published 2025)
- **DOI/URL**: https://arxiv.org/abs/2512.20655
- **인용수**: ~5

## 핵심 요약
IC 마스크 최적화 AI 연구를 위한 최대 규모 벤치마크 데이터셋 MaskOpt를 구축하고 공개한다. 45nm 노드 실제 IC 설계에서 추출한 메탈 레이어 104,714개 타일과 비아 레이어 121,952개 타일로 구성된다. 표준 셀 계층성(cell hierarchy)과 주변 패턴 문맥(context)을 보존하여 실제 산업 마스크 최적화 조건을 반영하며, SOTA 딥러닝 마스크 최적화 모델들의 체계적 벤치마크를 제공한다.

## 주요 기여
1. 최대 규모 실제 IC 설계 기반 마스크 최적화 데이터셋 (226,666 타일)
2. 표준 셀 계층성 + 주변 문맥 보존으로 실제 OPC 조건 반영
3. SOTA 딥러닝 마스크 최적화 모델 체계적 벤치마크
4. 컨텍스트 크기 분석 + 입력 어블레이션으로 주변 패턴의 중요성 실증

## Recipe/Process Flow 상세

### 기존 데이터셋의 한계
```
기존 마스크 최적화 데이터셋:
  합성 레이아웃 기반:
    임의 생성 패턴 → 실제 IC 설계와 다름
    표준 셀 구조 부재 → 반복 셀 패턴 미반영
  주변 문맥 부재:
    클립 타일만 최적화 → 인근 패턴 영향 무시
    실제: 수십 μm 범위 패턴이 OPC에 영향
  소규모:
    수천~수만 샘플 → 딥러닝 일반화 부족

MaskOpt 목표:
  실제 IC 설계 → 실용적 데이터셋
  대규모: 딥러닝 훈련/평가 충분
  표준 셀 계층성 + 문맥 보존
  공개 벤치마크: 재현 가능한 연구 환경
```

### 데이터셋 구성
```
원본 설계:
  45nm 노드 실제 IC 설계 (ASAP7 predictive PDK 기반)
  표준 셀 배치 + 라우팅 완료 레이아웃

타일 추출:
  메탈 레이어: 104,714 타일
  비아 레이어: 121,952 타일
  총: 226,666 타일

타일 크기:
  기본 타일: 표준 셀 경계 기반 추출
  컨텍스트 포함: 여러 컨텍스트 윈도우 크기 지원
    - 작은 컨텍스트: 근접 셀 포함
    - 큰 컨텍스트: 더 넓은 주변 패턴 포함

레이블 생성:
  각 타일 → OPC/ILT 실행 → 최적화 마스크 생성
  Ground Truth: 표준 ILT 결과
  시뮬레이션: TorchLitho Hopkins 광학 모델
```

### 표준 셀 계층성 보존
```
표준 셀 반복성:
  IC 설계: 같은 셀 (인버터, NAND, NOR) 반복 사용
  동일 셀: OPC 결과 동일 → 재사용 가능
  셀 인식 입력: 셀 ID + 배치 정보 포함

MaskOpt 셀 인식:
  타일 추출 시 표준 셀 경계 정보 보존
  반복 셀: 셀 수준 OPC 캐싱 가능
  → 딥러닝 모델이 셀 패턴 학습 활용 가능
```

### 컨텍스트 분석
```
컨텍스트 크기 실험:
  컨텍스트 없음 (타겟만): 낮은 OPC 품질
  소규모 컨텍스트: 근접 효과 일부 포착
  대규모 컨텍스트: OPC 품질 최대 (성능 포화점 존재)
  → 근접 효과 범위 (수 μm) 이상 컨텍스트 필요

입력 어블레이션:
  컨텍스트 없이 타겟만: 기준
  컨텍스트 + 셀 정보 추가: 유의미한 개선
  → 주변 패턴 + 셀 계층성 모두 중요
```

### SOTA 모델 벤치마크
```
평가 모델:
  Neural-ILT (CUHK, 2020)
  DevelSet (CUHK, 2021)
  GAN-OPC (CUHK, 2019)
  ILILT (ICML, 2024)

평가 지표:
  EPE (Edge Placement Error)
  PV Band (Process Variation Band)
  마스크 복잡도 (SRAF 수, 엣지 수)
  런타임

벤치마크 결과:
  모델별 트레이드오프 분석:
    ILILT: 낮은 EPE, 높은 계산 비용
    GAN-OPC: 빠름, 높은 EPE
  → 향후 연구 방향 제시
```

## OPC 툴 구현 관련성
- **SKOPC 훈련 데이터**: MaskOpt 데이터셋으로 SKOPC GNN-OPC, Neural-ILT 등 훈련/평가
- **벤치마크**: SKOPC OPC 품질을 MaskOpt 기준으로 공개 비교
- **표준 셀 OPC**: MaskOpt 셀 인식 입력으로 SKOPC 표준 셀 OPC 캐싱 구현
- **컨텍스트 윈도우**: OPC 타일 추출 시 적절한 컨텍스트 범위 결정에 MaskOpt 분석 활용

## 참고문헌
- arXiv:2512.20655 (December 2024)
- 관련: Neural-ILT (ICCAD 2020 / TCAD 2022)
- 관련: DevelSet (ICCAD 2021 / TCAD 2023)
- 관련: ILILT (ICML 2024)
- 관련: GAN-OPC (DAC 2018 / TCAD 2020)

## 태그
`Recipe`, `arxiv`, `Dataset`, `MaskOptimization`, `OPC`, `ILT`, `LargeScale`, `Benchmark`, `StandardCell`, `Context`, `DeepLearning`, `45nm`, `2025`
