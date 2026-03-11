# High-NA EUV Optical Proximity Correction Modeling Flow

## 메타데이터
- **저자**: (SPIE Photomask Technology 2025, 발표 13687-38)
- **연도**: 2025
- **게재지**: Proc. SPIE 13687, Photomask Technology 2025, 136870Q
- **DOI/URL**: https://doi.org/10.1117/12.3072706

## 핵심 요약
NA 0.55의 High-NA EUV 리소그래피 장비를 이용한 in-die 스티칭 실용화에 필수적인 완전한 공정 모델링 및 OPC 플로우를 구축한 연구. 비대칭 투영계(x: 4×, y: 8×)와 스티칭 요구사항을 포함한 High-NA EUV 전용 OPC 모델링 플로우를 처음부터 끝까지 체계적으로 기술한다.

## 주요 기여
1. **High-NA EUV 전용 OPC 플로우**: 0.55NA 비대칭 광학계에 맞는 완전한 모델-기반 OPC 플로우 구축
2. **비대칭 광학 모델**: x방향(4×)과 y방향(8×) 서로 다른 축소율을 처리하는 분리 모델링
3. **스티칭 OPC 통합**: in-die 스티칭 영역에 대한 OPC 보정 전략 포함
4. **마스크 3D 효과**: High-NA EUV에서 더욱 심화되는 mask 3D topography 효과 모델 통합
5. **검증 전략**: High-NA EUV 프린팅 결과 대비 OPC 모델 예측 정확도 평가

## Recipe/Flow 상세
- **High-NA EUV OPC 모델링 플로우**:
  1. **광학 파라미터 정의**:
     - NA = 0.55 (High-NA EUV)
     - 비대칭 축소율: x=4×, y=8×
     - 조명 조건: dipole, annular 등 High-NA 최적화 조명
  2. **마스크 모델**:
     - Mask 3D 효과: RCWA 기반 rigorous 시뮬레이션 보정
     - 흡수체 사이드월 각도, 두께 효과
     - EUV 특유의 shadowing 효과 (경사 조명)
  3. **레지스트 모델 캘리브레이션**:
     - High-NA용 캘리브레이션 패턴 설계 (비대칭 고려)
     - SEM 측정 데이터 기반 캘리브레이션
  4. **OPC 적용**:
     - 반 필드 단위 독립 OPC
     - 스티칭 영역 특수 보정
     - 비대칭 fragment 크기 설정
  5. **Post-OPC 검증**: 시뮬레이션 및 웨이퍼 프린팅 결과 비교
- **핵심 과제**:
  - 비대칭 축소율에 따른 OPC fragment 크기 조정 (x/y 방향 독립)
  - 스티칭 경계 양쪽 패턴의 연속성 보장
  - 마스크 스케일링 8× 정밀도와 OPC 수렴성

## OPC 툴 구현 관련성
- High-NA EUV 비대칭 광학 모델 구조 (`optical_model.py` x/y 분리 처리)
- 스티칭 경계 영역 OPC 레시피 설계 참고
- Mask 3D 모델 통합 방법 (Hopkins vs rigorous 선택 기준)
- SKOPC 모델링 모듈의 EUV 확장 로드맵에 직접 활용 가능

## 태그
`HighNA_EUV`, `OPC`, `ModelingFlow`, `0.55NA`, `Anamorphic`, `Stitching`, `Mask3D`, `SPIE`, `2025`
