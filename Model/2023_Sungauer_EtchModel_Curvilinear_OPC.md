# Etch Model Calibration and Usage in OPC Flow for Curvilinear Layouts

## 메타데이터
- **저자**: Elodie Sungauer, Laurent Depre, Raphael La Greca
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II
- **DOI/URL**: https://doi.org/10.1117/12.2657676

## 핵심 요약
ASML Tachyon OPC+ 플랫폼을 활용하여 곡선형(curvilinear) 레이아웃에 적합한 OPC 흐름을 구현한다. 에치 모델 교정 방법론, 모델 기반 에치 바이어스 보정의 OPC 구현, 전체 OPC 성능을 논의한다.

## 주요 기여
1. 곡선형 패턴(curvilinear layout)에 특화된 에치 모델 교정 방법론 제시
2. ASML Tachyon OPC+ 플랫폼에서의 모델 기반 에치 바이어스 보정 구현
3. 에치 편향 모델링 필요성을 정량적으로 입증
4. 전통적인 맨해튼 레이아웃에서 곡선형 레이아웃으로의 OPC 흐름 확장
5. 글로벌 OPC 성능 평가 및 에치 보정 전후 비교

## 모델 수식/아키텍처
- 에치 바이어스 모델: etch_bias = f(CD, pitch, shape_complexity, local_density)
- 곡선형 패턴 특성상 1D 피치/CD 외에 2D 패턴 기하학적 특성 파라미터 추가
- Tachyon OPC+ 내 에치 커널(etch kernel) 기반 컴팩트 모델 구조
- 리소그래피 모델과 에치 모델의 순차적 교정 및 결합 적용

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [ ] ML/DL
- [x] 하이브리드 (물리 기반 에치 컴팩트 모델)

## OPC 툴 구현 관련성
- ILT 및 curvilinear OPC가 요구되는 7nm 이하 노드에서 에치 모델 필수화
- SKOPC etch proximity correction 모듈 구현 시 참조 아키텍처
- Tachyon OPC+ 플랫폼의 에치 모델 통합 방식 이해에 직접 활용
- 곡선형 마스크 합성 흐름과 에치 보정의 공동 최적화 기반 제공

## 태그
`Model`, `Etch`, `Curvilinear`, `OPC`, `Calibration`, `Tachyon`, `SPIE`, `DTCO`
