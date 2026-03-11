# Etch Proximity Correction for Dense Array Patterns

## 메타데이터
- **저자**: Jian Wang, Sainan Yao, Yingchun Zhang
- **연도**: 2022
- **게재지**: Proc. SPIE 12052, Optical Microlithography XXXV, 2610743
- **DOI/URL**: https://doi.org/10.1117/12.2610743

## 핵심 요약
CD가 축소됨에 따라 에치 근접 효과(EPC)가 OPC에서 더 중요해진다. 밀집 어레이 패턴에서 마이크로로딩(microloading) 효과가 애퍼처 효과보다 중요해지는 현상을 연구하고, 밀집 어레이 패턴에 효과적인 밀도 규칙 테이블 기반 에치 근접 보정 방법을 제안한다.

## 주요 기여
1. 밀집 어레이 패턴에서 마이크로로딩 효과의 지배적 역할 규명
2. 고정 CD/피치 밀집 어레이의 밀도 효과 연구 및 정량화
3. 에치 모델 교정용 테스트 패턴 설계 방법론
4. 전통적 width/space 규칙 테이블 대신 밀도 규칙 테이블 개발
5. 밀집 어레이 패턴 EPC에서 밀도 규칙 테이블의 편리성과 효과성 입증

## 모델 수식/아키텍처
- **에치 근접 모델**:
  - 마이크로로딩 효과: etch_rate = f(local_pattern_density, loading_factor)
  - 밀도 규칙 테이블: density_bin → etch_bias_correction
  - CD 보정: CD_target = CD_design + B_etch(density)
- 밀도 계산: 반경 R 내의 레이아웃 면적 비율 ρ = A_feature / A_total
- 애퍼처 효과 vs. 마이크로로딩: CD 크기에 따른 지배 효과 전환 분석
- 테스트 패턴: 다양한 어레이 밀도 (0.1~0.9) × 고정 CD/피치

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [ ] ML/DL
- [x] 하이브리드 (물리 기반 밀도 규칙 에치 모델)

## OPC 툴 구현 관련성
- SKOPC 에치 근접 보정 모듈에서 밀집 어레이 전용 밀도 규칙 구현
- 메모리 소자(DRAM, NAND) 어레이 레이어의 에치 OPC 흐름 설계
- 마이크로로딩 효과를 고려한 EPC 규칙 테이블 생성 방법론
- `2014_Zavyalova_CombiningLithoEtch_OPC.md` 등 에치 모델 통합 연구의 밀집 어레이 특화 확장

## 태그
`Model`, `Etch`, `EPC`, `DenseArray`, `Microloading`, `OPC`, `DensityRule`, `Memory`, `SPIE`
