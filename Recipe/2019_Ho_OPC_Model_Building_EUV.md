# OPC Model Building for EUV Lithography

## 메타데이터
- **저자**: Benjamin C. P. Ho, Jonathan Doebler, Ardavan Niroomand
- **연도**: 2019
- **게재지**: Proc. SPIE 11147, International Conference on Extreme Ultraviolet Lithography 2019, 1114714
- **DOI/URL**: https://doi.org/10.1117/12.2531430

## 핵심 요약
EUV 리소그래피가 메모리 제조에 진입함에 따라, EUV aerial image 생성에 필요한 복잡한 물리 현상을 OPC 모델이 정확히 이해하고 보정해야 한다. 본 논문은 EUV OPC 모델 구축 과정에서 DUV 모델과의 차이점을 체계적으로 비교하고, 고량 생산(HVM)을 위한 EUV OPC 모델 빌딩의 핵심 과제들을 논의한다.

## 주요 기여
1. **EUV vs. DUV OPC 모델 비교**: EUV 특유의 물리 효과와 DUV 모델링 접근법의 차이 체계화
2. **비텔레센트릭 조명 shadowing**: 경사 조명에 의한 마스크 shadowing 효과의 OPC 모델 통합
3. **슬릿 가로 변동**: 스캐너 슬릿 방향 비균일성(across-slit variation)의 OPC 모델 반영
4. **Optical flare 보정**: EUV 시스템의 높은 flare 수준에 대한 모델 기반 보정
5. **Reticle black border 효과**: EUV 마스크의 불투명 테두리 효과 모델링

## Recipe/Flow 상세
- **EUV OPC 모델 빌딩 플로우**:
  1. **캘리브레이션 패턴 설계**:
     - EUV 특화 테스트 패턴: line/space, contact, 2D 패턴
     - Shadowing 민감도 패턴 (수평/수직 방향별)
     - Flare 민감도 패턴 (다양한 밀도)
  2. **EUV 특화 효과 측정**:
     - Shadowing: 마스크 방향에 따른 CD 비대칭 측정
     - Across-slit variation: 슬릿 위치별 CD 차이 측정
     - Flare: 패턴 밀도별 CD shift 측정
  3. **OPC 모델 파라미터 피팅**:
     - 표준 Hopkins 모델 + EUV 보정항
     - Shadowing 보정: 마스크 기울기 의존 bias
     - Flare 보정: 패턴 밀도 가중 convolution 항
  4. **모델 검증**:
     - 독립 검증 패턴으로 예측 정확도 확인
     - Full-chip OPC 적용 후 웨이퍼 프린팅 결과 비교
- **EUV OPC 모델 특수 파라미터**:
  - Shadowing coefficient: 흡수체 두께, 조명 각도 의존
  - Flare kernel: 스캐너별 flare 분포 함수
  - Across-slit polynomial: 슬릿 위치 의존 CD shift
- **메모리 vs. 로직**: EUV 메모리 제조 진입에 따른 고밀도 패턴 모델 필요성

## OPC 툴 구현 관련성
- SKOPC EUV 광학 모델에 shadowing, flare, across-slit 보정 추가 구조
- `euv_optical_model.py`: DUV 모델 기반 위에 EUV 특화 효과 레이어 추가
- 캘리브레이션 패턴 설계 기준 (EUV 특화 패턴 포함)
- HVM EUV OPC 모델의 정확도 요구사항 이해

## 태그
`EUV`, `OPC`, `ModelBuilding`, `Shadowing`, `Flare`, `Calibration`, `HVM`, `Memory`, `SPIE`, `2019`
