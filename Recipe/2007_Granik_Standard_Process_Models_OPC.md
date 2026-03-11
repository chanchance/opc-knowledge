# Toward Standard Process Models for OPC

## 메타데이터
- **저자**: Yuri Granik, Dmitry Medvedev, Nick Cobb
- **연도**: 2007
- **게재지**: Proc. SPIE 6520, Optical Microlithography XX, 652043
- **DOI/URL**: https://doi.org/10.1117/12.712229
- **인용수**: ~60

## 핵심 요약
OPC 및 OPC 검증용으로 설계된 CM1(Compact Model 1) 레지스트 모델을 제시하며, 칩 규모 공정 시뮬레이션을 위한 표준 패턴 전달 모델로 CM1을 제안한다. 모델 공식화, 저항 측정값과의 비교, 표준화 필요성을 논의한다.

## 주요 기여
1. OPC용 CM1(Compact Model 1) 레지스트 모델 공식화
2. 물리/화학적 과정을 보다 완전히 표현하는 분리 가능 모델 구조 제안
3. 실험 측정값과의 비교를 통한 모델 검증
4. 칩 규모 공정 시뮬레이션용 표준 모델 프레임워크 제안

## Recipe/Process Flow 상세

### CM1 모델 구조 (Compact Model 1)
```
전통적 OPC 모델 구조:
Resist_CD = f(Aerial_Image)

CM1 분리 가능 모델:
단계 1: 광학 이미지
  I(x,y) = Σ_k Σ_m TCC(k,m) · M̃(k) · M̃*(m)
  (Hopkins 공식, TCC: Transmission Cross Coefficient)

단계 2: 레지스트 모델 (물리/화학 분리)
  a) 노광 (Exposure):
     E(x,y) = I(x,y) ^ kernel_exposure
     (공간 이미지 → 노광 분포)

  b) PEB (Post-Exposure Bake) 확산:
     A(x,y) = E(x,y) ⊗ G_PEB(σ_PEB)
     (확산 커널로 블러링)

  c) 현상 (Development):
     CD_resist = threshold(A(x,y), t_resist)
     (임계값으로 이진화)

단계 3: 에칭 모델 (선택적)
  CD_wafer = f_etch(CD_resist)
```

### 모델 캘리브레이션 절차
```
1. 측정 데이터 수집
   - SEM CD 측정: 1D 라인-스페이스 (다양한 pitch/CD)
   - 2D 패턴: line-end, contact/via
   - 공정 윈도우 포인트: 다양한 초점/노광량 조합

2. 광학 모델 파라미터 결정
   - 광원 프로파일 측정 (Aerial Image Measurement System)
   - NA, σ (partial coherence) 설정
   - Aberration 측정 및 보정

3. 레지스트 모델 파라미터 최적화
   최소화: Σ |CD_measured - CD_modeled|^2
   변수: t_resist, σ_PEB, 확산 커널 파라미터

4. 모델 검증
   - 검증 패턴 세트에서 모델 예측 vs. 측정값
   - RMS 오차 < 기준값 (보통 < 1-2nm)
```

### 표준화 필요성 논의
```
현재 문제점:
- 각 EDA 업체마다 독자적 모델 공식화
- 모델 간 이식성 없음
- 캘리브레이션 방법 비표준화

CM1 표준화 제안:
- 공개된 모델 공식
- 표준 캘리브레이션 프로토콜
- OPC 툴 간 모델 공유 가능
```

## OPC 툴 구현 관련성
- **SKOPC 프로세스 모델**: `skopc/core/process_model.py`의 리소그래피 모델이 CM1 구조를 따름
- **캘리브레이션**: OPC 모델 캘리브레이션 절차의 표준 참조
- **분리 가능 구조**: 광학 + PEB확산 + 현상의 분리 가능 모델은 SKOPC의 LithoEngine 구조와 동일
- **Mentor Graphics**: Calibre OPC 모델의 이론적 기반 제공

## 참고문헌
- Proc. SPIE 6520, Optical Microlithography XX (2007)
- 저자 소속: Mentor Graphics Corp.
- 관련: SEM-contour-based OPC model calibration (SPIE 6518, 2007)
- 관련: Separable OPC models for computational lithography (SPIE 7028, 2008)

## 태그
`Recipe`, `SPIE`, `ModelCalibration`, `ResistModel`, `CM1`, `CompactModel`, `OPC-Model`, `StandardModel`, `MentorGraphics`, `Hopkins`
