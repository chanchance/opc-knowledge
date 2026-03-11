# LLM-HD: Layout Language Model for Hotspot Detection with GDS Semantic Encoding

## 메타데이터
- **저자**: (저자명 확인 필요 — DAC 2024 게재)
- **연도**: 2024
- **게재지/학회**: 61st ACM/IEEE Design Automation Conference (DAC 2024)
- **DOI/URL**: https://dl.acm.org/doi/10.1145/3649329.3658479
- **인용수**: 미확인

## 핵심 요약
GDS 이진 파일을 직접 처리하는 새로운 레이아웃 핫스팟 검출 패러다임을 제안한다. 기존 방법들이 GDS를 픽셀 이미지로 변환하면서 공간적·구조적 정보를 손실하는 문제를 해결하기 위해, 계층적 GDS 시맨틱 표현 체계와 사전 학습된 자연어 처리(NLP) 모델을 결합한다. GDS 기반 계층적 시맨틱 인코딩을 통해 반도체 레이아웃 데이터를 언어 모델이 처리할 수 있는 형태로 변환하고, 픽셀 변환 없이 GDS 이진 파일에서 직접 핫스팟을 검출함으로써 정확도와 효율성 모두에서 눈에 띄는 향상을 달성한다.

## 주요 기여
- **GDS 직접 처리 패러다임**: 픽셀 변환 없이 GDS 이진 파일에서 직접 핫스팟 검출
- **계층적 GDS 시맨틱 인코딩**: GDS의 계층적 구조 정보를 보존하는 시맨틱 표현 체계
- **사전 학습 NLP 모델 적용**: 자연어 처리용 사전 학습 언어 모델을 레이아웃 분석에 적응
- **공간·구조적 정보 보존**: 이미지 변환 시 손실되는 중요한 공간 및 구조 정보 유지
- **정확도·효율성 동시 향상**: 기존 픽셀 기반 방법 대비 두 지표 모두에서 향상

## 검증 방법론
- **ICCAD 벤치마크 평가**: 표준 핫스팟 검출 벤치마크로 GDS 직접 처리 성능 평가
- **픽셀 기반 방법 비교**: 기존 이미지 변환 기반 핫스팟 검출 방법들과 직접 비교
- **GDS 처리 정확도**: GDS 계층 구조 파싱 및 시맨틱 인코딩의 정확도 검증
- **속도 비교**: GDS 직접 처리 vs. 이미지 변환 후 처리의 속도 비교
- **절제 연구**: GDS 시맨틱 인코딩의 각 구성 요소가 성능에 미치는 영향 측정

## 검증 지표
- **정확도**: GDS 기반 핫스팟 분류 정확도 (기존 방법 대비 향상)
- **False Alarm Rate**: 비핫스팟을 핫스팟으로 오탐하는 비율
- **Miss Rate**: 실제 핫스팟을 놓치는 비율
- **처리 속도**: GDS 파일 처리 및 핫스팟 검출 전체 파이프라인 속도
- **사용 시뮬레이터**: ICCAD 벤치마크 시뮬레이터 기반 핫스팟 라벨링
- **검증 커버리지**: ICCAD 벤치마크 데이터셋 (GDS 형식 레이아웃 클립)

## OPC 툴 구현 관련성
SKOPC의 GDS 기반 OPC 검증 및 핫스팟 검출 모듈에 직접 활용 가능:
1. **GDS 직접 검증**: SKOPC의 GDS 레이아웃 파일에서 픽셀 변환 없이 직접 핫스팟 검출
2. **계층적 GDS 분석**: GDS 셀 계층 구조(cell hierarchy)를 활용한 OPC 검증 효율화
3. **언어 모델 기반 패턴 분석**: 사전 학습 언어 모델의 패턴 인식 능력을 레이아웃 분석에 적용
4. **GDS 시맨틱 인코딩**: SKOPC의 gdstk 기반 GDS 처리를 LLM-HD의 시맨틱 인코딩으로 확장
5. **OPC 후 자동 검증**: OPC 완료 후 GDS 출력 파일에서 자동으로 핫스팟 검출

## 참고문헌 (핵심)
- Geng et al. (2022) - Attention-based deep layout metric learning (TCAD)
- ICCAD 2012/2019 핫스팟 벤치마크 데이터셋
- GDS 포맷(GDSII) 표준 관련 참고문헌
- BERT/GPT 등 사전 학습 언어 모델 기초 연구
- Yang et al. (2017) - Imbalance aware hotspot detection

## 태그
`Verification`, `OPC`, `Hotspot Detection`, `LLM`, `Large Language Model`, `GDS`, `Semantic Encoding`, `DAC`, `2024`, `NLP`, `Layout Analysis`, `Direct Processing`, `Hierarchy`
