# Advanced Regression OPC Model Setup

## 메타데이터
- **저자**: Tony Hu, Terry Hsuan, Elvis Yang, Li-Jin Chen, Tony Chao, Y. P. Liao, Elsley Tan
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295419
- **DOI/URL**: https://doi.org/10.1117/12.3008958

## 핵심 요약
기존 모델 교정 기법(광학 모델 최적화 + 레지스트 모델 최적화)을 초기 모델로 설정한 후 고급 회귀 기법으로 OPC 모델 셋업을 개선하는 방법을 제안한다. 정확도와 안정성을 동시에 향상시키는 실용적인 모델 셋업 절차를 제공한다.

## 주요 기여
1. 기존 OPC 모델 교정의 단계별 접근(광학 → 레지스트)을 기반으로 한 고급 회귀 프레임워크
2. 초기 모델 품질이 최종 OPC 성능에 미치는 영향 분석
3. 회귀 기반 모델 파라미터 정제(refinement) 방법론
4. 모델 안정성(stability)과 예측 정확도의 트레이드오프 관리 전략
5. 산업 공정 OPC 모델 셋업 실무 가이드라인 제공

## 모델 수식/아키텍처
- **초기 광학 모델**: Hopkins TCC 기반 커널 분해, 주요 커널 수 최적화
- **초기 레지스트 모델**: CM1/CM0 계열 컴팩트 모델 파라미터 초기화
- **고급 회귀**: 전체 파라미터 공간의 비선형 최적화 (L-BFGS, 레벤버그-마쿼트)
- 교정 게이지(calibration gauge) 선택 전략: 패턴 다양성과 데이터 품질 균형
- 검증(validation) 세트 기반 모델 과적합 방지

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC 모델 교정 파이프라인의 표준 절차 구현 시 직접 참조
- 광학 모델 → 레지스트 모델 순차 최적화의 산업 표준 방법론
- 모델 교정 자동화(AutoOPC) 흐름 설계 시 기반 프레임워크
- Calibre, Tachyon 등 상용 OPC 툴의 모델 셋업 방식과 비교 가능

## 태그
`Model`, `Calibration`, `Regression`, `OPC`, `OpticalModel`, `ResistModel`, `ModelSetup`, `SPIE`, `DTCO`
