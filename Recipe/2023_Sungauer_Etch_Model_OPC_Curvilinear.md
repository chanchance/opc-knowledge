# Etch Model Calibration and Usage in OPC Flow for Curvilinear Layouts

## 메타데이터
- **저자**: Elodie Sungauer, Laurent Depre, Raphael La Greca
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124951H
- **DOI/URL**: https://doi.org/10.1117/12.2657676

## 핵심 요약
광학 소자(photonics) 제조에서 비전통적 curvilinear 형상의 웨이퍼 패터닝에는 ~100nm CD 수준에서 정확한 proximity 보정이 필요하다. ASML Tachyon OPC+ 플랫폼을 이용하여 curvilinear 레이아웃에 특화된 etch 모델 캘리브레이션 방법론과 OPC 플로우를 제시한다. 계측 전략, 모델 기반 etch bias 보정의 OPC 통합, 전체 OPC 성능을 체계적으로 다룬다.

## 주요 기여
1. **Curvilinear 특화 Etch 모델 캘리브레이션**: 곡선 형상 레이아웃에 맞는 etch 모델 개발 방법론
2. **계측 전략**: Curvilinear 패턴의 CD 측정을 위한 최적 계측 방법 정의
3. **Model-based Etch Bias 보정의 OPC 통합**: etch 보정을 OPC 루프에 통합하는 구현 방법
4. **실리콘 포토닉스 적용**: 광학 소자용 curvilinear 패턴 OPC에 적용한 실용적 결과
5. **Tachyon OPC+ 플랫폼**: ASML의 curvilinear OPC 전용 플랫폼 활용 사례

## Recipe/Flow 상세
- **Curvilinear Etch 모델 기반 OPC 플로우**:
  1. **계측 전략 수립**:
     - Curvilinear 패턴 대표 샘플 선정 (다양한 곡률, CD, 방향)
     - SEM 계측 위치 최적화 (곡선 구간 샘플링)
     - Resist 후 + etch 후 CD 쌍 수집
  2. **Etch 모델 캘리브레이션**:
     - Curvilinear 형상의 etch 근접 효과 특성화
     - 곡률 의존성 etch bias 파라미터 추출
     - 모델: 국소 밀도 + 형상 특징 기반 etch bias 예측
  3. **OPC 플로우 통합 (Tachyon OPC+)**:
     - 광학 모델 캘리브레이션 (curvilinear 특화)
     - Etch bias 보정을 OPC 타겟 보정 단계로 통합
     - Curvilinear 형상의 OPC 수렴 루프 실행
  4. **전체 OPC 성능 평가**:
     - EPE, CD 균일도, 공정 창 측정
     - Curvilinear MRC 준수 여부 확인
- **실리콘 포토닉스 특성**:
  - 비전통적 형상: 환형(ring), 나선형(spiral), 테이퍼(taper) 등
  - ~100nm CD: DUV 리소그래피 범위
  - 곡률 의존 etch bias: 볼록/오목 곡선에 따른 etch 속도 차이
- **Tachyon OPC+ 특징**: Curvilinear 형상 네이티브 처리 지원

## OPC 툴 구현 관련성
- 실리콘 포토닉스용 curvilinear OPC 레시피 설계 (SKOPC 확장 고려)
- 곡률 의존 etch bias 모델 구현 방법
- `curvilinear_etch_opc.py`: 곡률 계산 → etch bias 보정 → OPC 수렴 파이프라인
- 비전통적 형상(포토닉스) OPC와 반도체 OPC 차이점 이해

## 태그
`CurvilinearMask`, `EtchModel`, `OPC`, `Calibration`, `Photonics`, `ModelBased`, `TachyonOPC`, `SPIE`, `2023`
