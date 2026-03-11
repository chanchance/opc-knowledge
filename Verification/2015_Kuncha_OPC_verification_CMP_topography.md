# OPC Verification Considering CMP Induced Topography

## 메타데이터
- **저자**: Rakesh Kumar Kuncha, Aravind Narayana Samy, Ushasree Katakamsetty
- **연도**: 2015
- **게재지**: Proc. SPIE 9661, 31st European Mask and Lithography Conference, 96610E
- **DOI/URL**: https://doi.org/10.1117/12.2196646

## 핵심 요약
CMP(Chemical Mechanical Planarization)에 의해 유발된 웨이퍼 토포그래피(topography)가 리소그래피 포커스에 미치는 영향을 OPC 검증 플로우에 통합하는 방법론을 제안한 논문. CMP에 의한 토포그래피 기인 포커스 시프트(focus shift)를 OPC 검증의 공정 윈도우 조건에 반영함으로써, 실제 웨이퍼에서 발생하는 hotspot과의 상관관계를 개선하고 불필요한 false alarm을 감소시켰다.

## 주요 기여
1. **CMP 토포그래피 기인 포커스 시프트 모델**: CMP 공정 후 웨이퍼 표면 고저차에 의한 로컬 포커스 편차를 모델화
2. **OPC 검증 플로우 통합**: 토포그래피 기인 포커스 시프트를 OPC 검증의 공정 윈도우(nominal + 코너 조건)에 통합
3. **실제 웨이퍼 hotspot 상관관계 개선**: 토포그래피 반영 후 OPC 검증 hotspot과 실제 웨이퍼 결함 간의 예측 일치율 향상
4. **런타임 최소화**: 기존 OPC 검증 플로우에 최소한의 런타임 추가로 토포그래피 효과 반영
5. **다양한 제품 실증**: 여러 실제 제품 레이아웃에서 토포그래피 인식 OPC 검증의 개선 효과 검증

## 검증 방법론
- CMP 시뮬레이션 또는 계측으로 얻은 웨이퍼 토포그래피 맵을 OPC 검증 입력으로 활용
- 토포그래피 반영 전후 OPC 검증 hotspot과 실제 웨이퍼 결함 간의 상관관계 비교
- False positive/negative 비율 개선 정량화
- 다중 제품에서 토포그래피 인식 검증 방법의 일반화 성능 평가

## OPC 툴 구현 관련성
- SKOPC의 OPC 검증 모듈에 CMP 토포그래피 맵 입력 기능 및 포커스 시프트 보정 추가 시 핵심 참조
- 토포그래피 기인 포커스 편차를 공정 윈도우 분석(PWO)에 통합하는 SKOPC PWO 모듈 확장 근거
- `2007_Lee_LRC_process_window_error_detection.md`(기수집)의 LRC 기반 공정 윈도우 검증을 CMP 효과를 포함하여 확장
- 풀칩 OPC 검증에서 레이어별 토포그래피 의존 포커스 시프트를 고려하는 검증 파라미터 설계 기준

## 태그
`Verification`, `SPIE`, `CMP`, `Topography`, `OPC`, `Focus Shift`, `Process Window`, `Hotspot`, `LRC`
