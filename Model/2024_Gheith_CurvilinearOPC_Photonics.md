# An Overview of Curvilinear OPC Algorithms for Silicon Photonics Applications

## 메타데이터
- **저자**: Mohamed Gheith
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III
- **DOI/URL**: https://doi.org/10.1117/12.3025295

## 핵심 요약
CMOS 마이크로전자공학 대비 실리콘 포토닉스 설계에서의 OPC 및 etch 보정의 고유한 도전 과제를 종합적으로 검토한다. 실리콘 포토닉스 기술이 초기 개발 단계에서 고볼륨 제조(HVM)로 전환됨에 따라 커브선형(curvilinear) OPC 알고리즘의 적용이 필요해짐을 논증한다.

## 주요 기여
- 실리콘 포토닉스 vs. 기존 CMOS 설계에서의 OPC 도전 과제 체계적 비교
- 포토닉스 디자인(경사 에지, 커브 패턴)에 적합한 curvilinear OPC 알고리즘 검토
- HVM 전환에 따른 OPC 솔루션 요구사항 분석
- 180nm 실리콘 포토닉스 노드에서의 curvilinear OPC 적용 사례
- 포토닉스 특화 MRC(Mask Rule Check) 및 etch 보정 방법론

## 모델 수식/아키텍처
- Curvilinear OPC: Bézier 또는 spline 기반 세그먼트로 마스크 경계 표현
- 포토닉스 디바이스 특화 proximity correction 모델
- 기존 Manhattan geometry OPC와 curvilinear OPC의 알고리즘 비교
- 100nm 전후 CD를 갖는 포토닉스 패턴에 대한 advanced lithography process 적용

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC Layout Editor의 실리콘 포토닉스 지원 확장 시 참조 알고리즘
- Curvilinear OPC 구현에서 포토닉스 특화 MRC 고려 방향 제시
- 180nm 노드 포토닉스 플랫폼의 OPC 솔루션 개발 기준 문서

## 태그
`Model`, `SPIE`, `Curvilinear OPC`, `Silicon Photonics`, `HVM`, `CMOS`, `Etch Correction`, `DTCO`
