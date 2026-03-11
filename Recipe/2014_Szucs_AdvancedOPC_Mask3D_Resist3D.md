# Advanced OPC Mask-3D and Resist-3D Modeling

## 메타데이터
- **저자**: A. Szucs, J. Planchot, V. Farys, E. Yesilada (STMicroelectronics); L. Depre, S. Kapasi (ASML Brion); C. Gourgon, M. Besacier (LTM-CNRS, CEA); O. Mouraille, F. Driessen (ASML Netherlands)
- **연도**: 2014
- **게재지**: Proc. SPIE 9052, Optical Microlithography XXVII, 905208
- **DOI/URL**: https://doi.org/10.1117/12.2047281
- **인용수**: ~30

## 핵심 요약
28nm 메탈 레이어에서 복잡한 2D 레이아웃 구조의 OPC 정확도를 향상시키기 위해 마스크-3D(Mask-3D) 및 레지스트-3D(Resist-3D) 모델을 결합한 고급 OPC 모델링 방법론을 제시한다. STMicroelectronics + ASML Brion + CEA-CNRS 공동 연구로, 마스크 두께 효과와 레지스트 3D 단면 효과를 OPC 컴팩트 모델에 통합하여 2D 패턴에서의 모델 예측 오차를 감소시킨다.

## 주요 기여
1. Mask-3D와 Resist-3D 효과의 OPC 모델 동시 통합
2. 28nm 메탈 레이어 2D 패턴에서 모델 예측 오차 감소
3. 컴팩트 모델 형태로 3D 효과 근사 (풀칩 OPC에 적용 가능한 속도)
4. STMicroelectronics + ASML Brion + CEA-CNRS 산학연 협력 검증

## Recipe/Process Flow 상세

### Mask-3D 및 Resist-3D 효과와 OPC 모델의 연관성
```
표준 OPC 모델 가정:
  마스크: 무한히 얇은 이진 투과율 마스크 (Kirchhoff 근사)
  레지스트: 2D 임계값 모델 (단순 문턱값 이진화)

28nm 이하에서 두 가정 모두 부적절:

  Mask-3D 효과:
    - 마스크 흡수체 두께(60-80nm)가 파장(193nm)에 비해 무시 불가
    - 비수직 입사 → 두께에 의한 위상 오차
    - H/V 방향 마스크 패턴 간 비대칭 이미징
    - 2D 패턴(코너, 끝단)에서 효과 두드러짐

  Resist-3D 효과:
    - 레지스트 상부(top)와 하부(bottom)의 CD 차이
    - Resist top-loss: 레지스트 두께 감소 (노광 중)
    - 측벽 각도(sidewall angle): 2D 단면 형상
    - 이미지 로그 기울기(ILS) → 측벽 각도 결정
```

### Mask-3D 및 Resist-3D 모델 구축
```
Mask-3D 컴팩트 모델:
  완전 EM 시뮬레이션 (RCWA): 기준 데이터 생성
    → Rigorous mask model: 정확하지만 느림 (풀칩 불가)

  컴팩트 근사:
    1. 방향-의존 근접 보정항 추가
       ΔCD_M3D = f(CD, pitch, orientation)
    2. Lookup 테이블 또는 다항식 근사
    3. EM 시뮬 결과로 테이블 캘리브레이션

Resist-3D 컴팩트 모델:
  Resist 공정 시뮬레이션: PEB + 현상 단계 포함
    → 레지스트 단면 프로파일 (top CD, bottom CD)

  컴팩트 근사:
    1. Top/Bottom CD 차이 = f(ILS, dose)
    2. Resist top-loss 보정항: ΔCD_R3D = g(ILS, dose)
    3. 2D 패턴: 이방성 top-loss 처리
```

### 통합 OPC 캘리브레이션 흐름
```
1단계: 기준 데이터 생성
  - 다양한 1D + 2D 패턴 (SEM 측정)
  - 마스크-3D 기준: RCWA 시뮬레이션 결과
  - 레지스트-3D 기준: AFM 단면 또는 TEM 측정

2단계: 표준 모델 캘리브레이션
  - 광학 파라미터 (NA, σ, aberration) 피팅
  - 레지스트 컴팩트 파라미터 (diffusion, bias) 피팅

3단계: M3D + R3D 보정항 추가
  - ΔCD_M3D: RCWA vs. Kirchhoff 잔차 피팅
  - ΔCD_R3D: 3D 레지스트 vs. 2D 레지스트 잔차 피팅
  - 합산: CD_model = CD_standard + ΔCD_M3D + ΔCD_R3D

4단계: 2D 패턴 검증
  - 코너, T-junction, 끝단(line-end) 패턴에서 검증
  - M3D+R3D 통합 모델 vs. 표준 모델 비교
```

### 성능 결과 (28nm 메탈 레이어)
```
1D 패턴 OPC 정확도:
  표준 모델: RMS EPE 기준값
  M3D+R3D 통합: 비슷하거나 소폭 개선

2D 패턴 OPC 정확도 (코너, 끝단):
  표준 모델: RMS EPE 높음 (M3D, R3D 효과 누락)
  M3D+R3D 통합: RMS EPE 감소 (2D 패턴 개선 두드러짐)

런타임:
  컴팩트 M3D+R3D 근사: 완전 EM 시뮬 대비 수십~수백 배 빠름
  풀칩 OPC에 적용 가능한 수준
```

## OPC 툴 구현 관련성
- **SKOPC 마스크 3D**: `skopc/core/litho_engine.py`에 마스크 두께 보정항(ΔCD_M3D) 추가 인터페이스
- **레지스트 3D**: `skopc/core/litho_engine.py`에 resist top-loss 및 측벽 각도 효과 컴팩트 모델
- **STMicro+ASML 검증**: 상용 공정의 실증 검증으로 신뢰도 높음
- **캘리브레이션 확장**: `skopc/modeling/` 모델 캘리브레이션에 3D 보정항 추가 최적화

## 참고문헌
- Proc. SPIE 9052, Optical Microlithography XXVII (2014)
- 저자 소속: STMicroelectronics + ASML Brion + LTM-CNRS, CEA
- 관련: Effect of mask 3D and scanner focus difference on OPC (SPIE 9052, 2014)
- 관련: Resist toploss modeling for OPC applications (SPIE 9052, 2014)
- 관련: EUV OPC modeling and correction requirements (SPIE 9048, 2014)

## 태그
`Recipe`, `SPIE`, `OPC-Modeling`, `Mask3D`, `Resist3D`, `CompactModel`, `28nm`, `STMicroelectronics`, `ASML`, `2DPattern`, `LineEnd`, `2014`
