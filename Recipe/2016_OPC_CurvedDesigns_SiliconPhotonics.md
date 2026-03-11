# OPC for Curved Designs in Application to Photonics on Silicon

## 메타데이터
- **저자**: (SPIE 9780 - 2016 SPIE Advanced Lithography)
- **연도**: 2016
- **게재지**: Proc. SPIE 9780, Optical Microlithography XXIX
- **DOI/URL**: https://doi.org/10.1117/12.2230400
- **인용수**: ~25

## 핵심 요약
실리콘 포토닉스(silicon photonics) 소자 제조를 위한 193nm 리소그래피에서 곡선(curved) 형상을 가진 포토닉 도파관(waveguide), 방향성 결합기(directional coupler), 링 공진기(ring resonator) 등에 OPC를 적용하는 방법론을 제시한다. 기존 CMOS용 Manhattan OPC와 달리 곡선 도파관의 기하학적 특성을 처리하는 특화 OPC 흐름을 개발하며, 포토닉 소자의 삽입 손실, 결합 계수, 공진 파장에 미치는 공정 변동 효과를 분석한다.

## 주요 기여
1. 곡선 포토닉 소자에 대한 OPC 흐름 개발 (기존 Manhattan OPC 확장)
2. 193nm DUV 리소그래피에서 포토닉 소자의 공정 충실도 향상
3. 포토닉 성능(삽입 손실, 결합 계수)과 리소그래피 OPC 간 연계 분석
4. 포토닉 친화적(photolithography-friendly) 소자 설계 지침 도출

## Recipe/Process Flow 상세

### 실리콘 포토닉스 OPC의 특수 요구사항
```
CMOS 리소그래피 vs. 실리콘 포토닉스:
  CMOS:
    - 주로 직교(Manhattan) 기하구조
    - CD 정확도: ±5-10% 허용
    - 기능: 전기적 (Vt, Ion 중요)

  실리콘 포토닉스:
    - 곡선, 테이퍼(taper), 나선(spiral) 형상
    - CD 정확도: 서브-nm 필요 (도파관 단면 폭에 직접 의존)
    - 기능: 광학적 (모드 필드, 결합 길이 중요)
    - 측벽 조도(sidewall roughness): 산란 손실에 민감

포토닉 OPC의 도전:
  - 곡선 반경에 따라 근접 효과가 변함
  - 도파관 단면 CD가 포토닉 성능에 직접 매핑
  - 곡선 형상의 Manhattan 분해 후 OPC 필요
  - ILT/MB-OPC 흐름 재설계 필요
```

### 포토닉 OPC 방법론
```
1단계: 포토닉 설계 전처리
  a) 곡선 경계를 충분한 분해능으로 다각형 근사
     원호(arc): 각도 해상도 ≤ 0.1° 또는 현 오차 ≤ 1nm
  b) GDS/OASIS 형식으로 저장

2단계: OPC 최적화 목표 설정
  CMOS OPC: CD 오차 최소화 (EPE)
  포토닉 OPC: 도파관 폭(W) 정확도 + 측벽 조도 최소화
    목표: W_actual = W_design ± ΔW_max
    측벽: Ra < R_max (최대 허용 조도)

3단계: Model-Based OPC 실행
  - 컴팩트 광학-레지스트 모델 캘리브레이션
  - 도파관 직선 구간, 곡선 구간 분리 처리
  - 곡선 구간: 곡률 의존 근접 효과 보정 테이블
  - SRAF: 포토닉 도파관의 격리 패턴에 적용

4단계: 포토닉 성능 검증
  - OPC 후 레이아웃 → 리소그래피 시뮬 → 도파관 CD 프로파일
  - 도파관 CD 프로파일 → FDTD 광학 시뮬 → 삽입 손실, 결합 계수
  - 성능 목표 달성 여부 확인
```

### 포토닉 소자 유형별 OPC 전략
```
직선 도파관 (Straight Waveguide):
  - 표준 1D OPC 적용
  - 선폭 바이어스 보정
  - Dense/isolated 간 CD 차이 보상

곡선 도파관 (Curved Waveguide):
  - 곡률 반경 R에 따른 내측/외측 비대칭 근접 효과
  - R > 5μm: 직선 OPC 유사
  - R < 5μm: 곡률 의존 보정 테이블 적용

방향성 결합기 (Directional Coupler):
  - 두 도파관 사이 간격(gap) 정확도가 결합 계수 결정
  - Gap OPC: 설계 gap → 목표 gap으로 재조정
  - Gap 변화 0.5nm → 결합 계수 수 % 변화

링 공진기 (Ring Resonator):
  - 링 반지름 정확도 → 공진 파장 이동
  - 링 폭 OPC + 링-버스 gap OPC 통합
```

### 성능 결과
```
OPC 전후 비교 (193nm DUV, SOI 플랫폼):
  도파관 CD 정확도:
    OPC 없음: ±5-15nm 편차
    OPC 있음: ±2-3nm로 감소

  삽입 손실 (1μm 폭 도파관):
    CD 오차 제거로 예측 가능한 손실 달성

  방향성 결합기 결합 계수:
    OPC로 설계값 대비 오차 감소
```

## OPC 툴 구현 관련성
- **SKOPC 포토닉 모드**: `skopc/modeling/` 포토닉 소자 전용 OPC 모드 추가 (곡선 처리)
- **곡선 도파관 분해**: `skopc/core/layout_db.py`에 원호 → 다각형 변환 유틸리티
- **CD-성능 연계**: 도파관 CD 프로파일 → 간단한 광학 성능 예측기 연동
- **포토닉 레시피**: YAML 레시피에 photonic_mode 파라미터로 포토닉 소자 전용 OPC 설정

## 참고문헌
- Proc. SPIE 9780, Optical Microlithography XXIX (2016)
- 관련: Design and optimization of photolithography friendly photonic components (SPIE 9751, 2015)
- 관련: Application of OPC for 193nm DUV enabled InP photonic ICs (ECIO, 2019)
- 관련: Curvilinear mask handling in OPC flow (SPIE 12495, 2023)

## 태그
`Recipe`, `SPIE`, `SiliconPhotonics`, `CurvedOPC`, `Waveguide`, `PhotonicIC`, `193nm`, `DirectionalCoupler`, `RingResonator`, `InsertionLoss`, `2016`
