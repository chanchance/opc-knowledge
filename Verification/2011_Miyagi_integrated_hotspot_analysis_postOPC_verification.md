# Integrated Advanced Hotspot Analysis Techniques in the Post-OPC Verification Flow

## 메타데이터
- **저자**: Makoto Miyagi, Peter Brooker, Chander Sawh, Travis Brist, Kunal Taravade
- **연도**: 2011
- **게재지**: Proc. SPIE 8166, Photomask Technology 2011, 81663P
- **DOI/URL**: https://doi.org/10.1117/12.900609

## 핵심 요약
Post-OPC 검증 플로우의 LRC(Lithography Rule Check) hotspot 검출 단계에 리고러스 리소그래피 시뮬레이션을 긴밀하게 통합하는 방법론을 제안한 논문. 컴팩트 모델 기반 LRC에서 발견된 hotspot에 대해 리고러스 모델을 적용하여 레지스트의 3D 현상 프로파일(developed profile)을 분석하고, OPC 보정 및 hotspot 처리(disposition)의 신뢰도를 높였다.

## 주요 기여
1. **리고러스 시뮬레이션 통합 LRC 플로우**: 기존 컴팩트 모델 LRC 후 리고러스 시뮬레이션을 보조적으로 적용하는 이중 계층 검증 아키텍처
2. **3D 레지스트 프로파일 인사이트**: 리고러스 모델이 제공하는 웨이퍼 수준 3D 현상 프로파일을 hotspot 분석에 활용
3. **Hotspot Disposition 개선**: 리고러스 시뮬레이션으로 컴팩트 모델 LRC의 false positive/negative를 필터링하여 처리 우선순위 개선
4. **OPC 보정 지원**: Hotspot 3D 분석 결과를 OPC 보정 루프에 피드백하는 통합 플로우
5. **런타임 효율화**: 전체 칩 영역에 컴팩트 모델 사용, 위험 영역에만 리고러스 시뮬레이션 집중 적용

## 검증 방법론
- 컴팩트 모델 LRC 결과와 리고러스 시뮬레이션 결과 비교 (false positive/negative 분석)
- 3D 레지스트 프로파일 시뮬레이션 대 실제 SEM cross-section 비교
- Hotspot 재현율(recall) 및 false alarm 비율로 통합 플로우 성능 평가
- LRC 단독 대비 리고러스 통합 플로우의 hotspot 발견 정확도 향상 정량화

## OPC 툴 구현 관련성
- SKOPC의 post-OPC 검증 모듈에서 2단계 검증(컴팩트 → 리고러스) 아키텍처 설계의 기초
- `2011_Miyagi_hotspot_analysis_post_OPC_verification.md`(기수집)와 같은 저자(Miyagi)의 동년 다른 논문으로 상호 보완적
- `2007_Lee_LRC_process_window_error_detection.md`(기수집)의 LRC 방법론을 리고러스 시뮬레이션으로 강화하는 후속 연구
- SKOPC 검증 플로우에서 hotspot 우선순위화(prioritization) 알고리즘 구현 시 참조

## 태그
`Verification`, `SPIE`, `Hotspot`, `LRC`, `Post-OPC`, `Rigorous Simulation`, `OPC`, `3D Resist Profile`, `Compact Model`
