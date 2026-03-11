# Enhancing OPC Accuracy in 28nm-Class Analog Devices: Addressing Degradation in Specific BEOL Patterns through Recipe Tuning and Simulation

## 메타데이터
- **저자**: Keeho Kim, Yi-Hao Huang, Mark Terry (Texas Instruments Inc.)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250J
- **DOI/URL**: https://doi.org/10.1117/12.3048585

## 핵심 요약
28nm급 아날로그 디바이스의 BEOL(Back-End-of-Line) 특정 패턴에서 발생하는 OPC 정확도 저하 문제를 진단하고, OPC 레시피 튜닝 및 시뮬레이션을 통해 해결하는 방법론을 제시한다. BEOL 공정에서 안정적인 수율을 확보하기 위해 공정 마진 확보가 핵심이며, 고정밀 OPC 달성을 위한 SMO(Source Mask Optimization), OPC 모델 개발, OPC 레시피 빌드, ORC(Optical Rule Check) 검증 및 웨이퍼 데이터 피드백 루프를 체계화한다.

## 주요 기여
1. **28nm 아날로그 BEOL OPC 정확도 향상**: 특정 BEOL 패턴에서 OPC 정확도 저하 원인 규명 및 해결
2. **OPC 레시피 튜닝 방법론**: 문제 패턴 대상 레시피 파라미터 최적화 전략 체계화
3. **SMO-OPC 통합 최적화**: 광원-마스크 공동 최적화와 OPC 레시피의 연계 최적화
4. **ORC 기반 검증 루프**: OPC 결과 ORC 검증 → 웨이퍼 데이터 수집 → 레시피 피드백 반복
5. **아날로그 디바이스 특화 OPC**: 로직/메모리와 다른 아날로그 BEOL 패턴 특성 반영

## Recipe/Flow 상세
- **28nm 아날로그 BEOL OPC 최적화 플로우**:
  1. **문제 패턴 진단**:
     - 특정 BEOL 패턴에서 OPC 정확도 저하 현상 파악
     - CD-SEM 측정 데이터와 OPC 시뮬레이션 결과 비교
     - 정확도 저하 원인: 비전형적 패턴 형상, 고립/밀집 편차, 에치 비선형성 등
  2. **SMO 튜닝**:
     - 문제 패턴에 최적화된 광원 조건 재설계
     - 조명 파라미터(σ, 형태, 강도 분포) 조정
     - 마스크 타입 및 에지 배치 최적화
  3. **OPC 모델 재개발**:
     - 문제 패턴 포함 캘리브레이션 게이지 설계
     - 광학 모델 및 레지스트 모델 정밀 캘리브레이션
     - 에치 근접 보정(EPC) 모델 통합
  4. **OPC 레시피 빌드 및 튜닝**:
     - 기존 레시피 파라미터(fragment 크기, 이동 제한, 수렴 조건) 재조정
     - 문제 패턴 전용 OPC 규칙 추가 (rule-based 보완)
     - Simulation-based 검증으로 레시피 효과 사전 확인
  5. **ORC 검증 및 웨이퍼 피드백**:
     - ORC(Optical Rule Check)로 수정된 OPC 결과 전수 검증
     - 웨이퍼 노광 → CD 측정 → OPC 정확도 재평가
     - 잔여 오차 분석 → 레시피 반복 개선
- **아날로그 BEOL 패턴 특성**:
  - 다양한 피치 혼재: 고립 패턴과 밀집 패턴이 혼재하는 아날로그 레이아웃
  - 비정형 형상: 표준 디지털 레이아웃과 다른 비정형 아날로그 패턴
  - 공정 마진 요구: 아날로그 소자 특성상 엄격한 CD 제어 필요
- **소속**: Texas Instruments Inc. (미국 텍사스)

## OPC 툴 구현 관련성
- SKOPC 아날로그 디바이스 전용 OPC 레시피 개발 참고 사례
- 특정 레이어/패턴 유형별 OPC 정확도 저하 진단 방법론 적용
- ORC 기반 OPC 품질 검증 루프 구현 기준
- 비전형적 BEOL 패턴 처리를 위한 OPC 레시피 튜닝 전략

## 태그
`OPC`, `AnalogDevice`, `BEOL`, `28nm`, `RecipeTuning`, `ORC`, `SMO`, `CDControl`, `Yield`, `TexasInstruments`, `SPIE`, `2025`
