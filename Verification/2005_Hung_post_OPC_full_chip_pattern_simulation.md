# Post-OPC Verification Using a Full-Chip Pattern-Based Simulation Verification Method

## 메타데이터
- **저자**: Chi-Yuan Hung, Ching-Heng Wang, Cliff Ma, Gary Zhang
- **연도**: 2005
- **게재지**: Proc. SPIE 5992, 25th Annual BACUS Symposium on Photomask Technology, 59922Z
- **DOI/URL**: https://doi.org/10.1117/12.632351
- **인용수**: 다수 (Post-OPC 전칩 검증 방법론 기준 논문)

## 핵심 요약
OPC 이후 전칩 레벨에서 패턴 기반 시뮬레이션 검증 기법을 활용한 신속하고 정확한 post-OPC 검증 방법론을 평가·조사한다. 0.13um, 0.11um, 90nm 기술 노드의 여러 데이터베이스에 대해 적용한 결과, 모델 기반 post-OPC 검사가 기존 검사에서 누락된 오류(OPC 데이터 오류)를 검출함으로써 제조 비용(레티클, 웨이퍼 공정, 생산 지연)을 절감할 수 있음을 입증한다.

## 주요 기여
1. 상용 플랫폼 기반 고속 전칩 post-OPC 검증 기법의 체계적 평가
2. 0.13um~90nm 다중 노드 OPC 데이터베이스에서 기존 검사가 놓친 OPC 오류 검출 실증
3. 패턴 기반 시뮬레이션과 모델 기반 검사의 상보적 활용 방법론 확립
4. OPC 검증 런타임과 정확도의 트레이드오프 분석 및 실용적 기준 제시

## 검증 방법론
- **패턴 기반 전칩 시뮬레이션**: 레이아웃 전체에 걸쳐 컴팩트 모델로 웨이퍼 윤곽선 시뮬레이션 수행
- **모델 기반 post-OPC 체크**: 시뮬레이션된 웨이퍼 컨투어와 설계 타겟 간 EPE 비교
- **오류 분류**: EPE 한계값 초과 패턴을 핫스팟으로 분류, 위험도별 우선순위 부여
- **알고리즘**: TCC 기반 광학 시뮬레이션 + 간소화 레지스트 모델 결합
- **적용 기술 노드**: 0.13um, 0.11um, 90nm 실제 칩 데이터베이스

## 검증 지표
- EPE 허용 범위: 각 노드별 CD 스펙 기준 (90nm 노드: 수 nm 수준)
- 시뮬레이터: 상용 전칩 시뮬레이션 플랫폼 (패턴 기반 ORC 계열)
- 커버리지: 수십 개의 실제 OPC 데이터베이스 전체 검증

## OPC 툴 구현 관련성
- **Post-OPC Verify 플로우의 핵심 참조 논문**: `VerificationEngine`의 전칩 EPE 검사 알고리즘 설계 시 직접 참조
- 패턴 기반 + 모델 기반 혼합 검증 아키텍처 구현의 기술적 근거 제공
- OPC 결과물의 sign-off 기준(EPE 임계값, 검출 민감도) 설정에 활용 가능
- 실제 제조 환경에서 OPC 오류 검출의 경제적 중요성을 수치로 제시한 기준 문헌

## 참고문헌
- SPIE BACUS Photomask Technology 2005, Vol. 5992
- 전칩 리소그래피 시뮬레이션 관련 선행 연구 다수

## 태그
`Verification`, `SPIE`, `PostOPC`, `FullChip`, `PatternBased`, `EPE`, `OPCSignOff`, `Hotspot`, `Simulation`
