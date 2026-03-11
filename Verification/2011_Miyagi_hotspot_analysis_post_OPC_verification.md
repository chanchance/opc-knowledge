# Integrated Advanced Hotspot Analysis Techniques in the Post-OPC Verification Flow

## 메타데이터
- **저자**: Makoto Miyagi, Peter Brooker, Chander Sawh, Travis Brist, Kunal Taravade
- **연도**: 2011
- **게재지**: Proc. SPIE 8166, Photomask Technology 2011, 81663P
- **DOI/URL**: https://doi.org/10.1117/12.900609
- **인용수**: 다수 (Post-OPC 핫스팟 분석 통합 플로우 기준 논문)

## 핵심 요약
Post-OPC 검증 플로우의 LRC 핫스팟 검출 단계에 정밀 리소그래피 시뮬레이션을 긴밀하게 통합하는 방법의 이점을 탐구한다. 다양한 사용자 플로우와 런타임 영향을 최소화하면서 이미지 예측 가능성(imaging predictability)을 극대화하는 자동화 방법을 제시한다. 컴팩트 LRC 모델과 리고러스(rigorous) 시뮬레이션의 상보적 활용 전략을 다룬다.

## 주요 기여
1. LRC 핫스팟 검출에 정밀 리소그래피 시뮬레이션을 통합하는 타이트한 결합 아키텍처 제안
2. 다중 사용자 플로우에 대한 자동화 방법 개발 — TAT(Turn-Around Time) 영향 최소화
3. 컴팩트 모델 LRC와 정밀 시뮬레이션의 계층적 결합으로 정확도·런타임 균형 달성
4. Photomask 제조 환경에서 post-OPC 검증 품질 향상의 실용적 경로 제시

## 검증 방법론
- **계층적 검증 플로우**:
  1. 1단계: 컴팩트 LRC 모델로 전칩 고속 핫스팟 후보 식별
  2. 2단계: 식별된 핫스팟 후보에 대해 정밀(rigorous) 리소그래피 시뮬레이션 적용
- **LRC 핫스팟 검출**: EPE 기반 오류 검출 + 공정 윈도우 마진 평가
- **정밀 시뮬레이션 통합**: 3D 마스크 효과(EMF), 스캐너 수차, 레지스트 모델 포함 고정밀 이미지 예측
- **자동화 플로우**: 핫스팟 후보 필터링 → 정밀 재검증 → 오류 등급 갱신의 자동 파이프라인
- **다중 플로우 지원**: 마스크 합성 sign-off, 공정 개발, 수율 모니터링 등 용도별 플로우

## 검증 지표
- EPE 허용 범위: 포토마스크 기술 노드 기준 (Photomask Technology 2011 대상 노드)
- 시뮬레이터: 컴팩트 LRC 엔진 + 정밀 리소그래피 시뮬레이터 (rigorous EMF 포함)
- 커버리지: 전칩 LRC + 선택적 정밀 검증 (2단계 필터링)

## OPC 툴 구현 관련성
- **2단계 검증 아키텍처 구현의 핵심 참조**: `VerificationEngine`에서 고속 컴팩트 검사 후 의심 패턴만 정밀 시뮬레이션하는 계층적 파이프라인 설계에 직접 활용
- 컴팩트 모델 기반 LRC와 정밀 시뮬레이션의 결합 방법 — 구현 난이도 대비 정확도 향상 방법론 제공
- 자동화 핫스팟 분류 및 우선순위 지정 알고리즘 구현의 실무 기준
- Photomask sign-off 플로우에서 검증 정확도와 TAT 균형을 맞추는 실용적 설계 지침

## 참고문헌
- SPIE Photomask Technology 2011, Vol. 8166
- Miyagi, Brooker 등 Mentor Graphics 계열 OPC 검증 연구

## 태그
`Verification`, `SPIE`, `PostOPC`, `Hotspot`, `LRC`, `RigorousSimulation`, `MaskSignOff`, `HierarchicalVerification`, `Automation`
