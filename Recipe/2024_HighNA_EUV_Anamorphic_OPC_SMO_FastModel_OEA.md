# Fast Source-Mask Co-Optimization Method for High-NA EUV Lithography

## 메타데이터
- **저자**: (Opto-Electronic Advances, 2024)
- **연도**: 2024
- **게재지**: Opto-Electronic Advances (OEA), 2024
- **DOI/URL**: https://www.oejournal.org/oea/article/doi/10.29026/oea.2024.230235
- **인용수**: ~15

## 핵심 요약
High-NA EUV 리소그래피(NA=0.55)의 아나모픽 광학계를 고려한 고속 소스-마스크 공동 최적화(SMO) 방법을 제안한다. 아나모픽 광학계의 비대칭 배율(x: 4×, y: 8×)로 인해 발생하는 마스크 오차 비대칭, M3D 효과, OPC 모델 복잡성 증가 등의 과제를 다루며, 마스크 3D 구조와 아나모픽 배율 효과를 포함하는 고속 High-NA EUV 이미징 모델을 구축하여 실용적인 전체 칩 SMO를 가능하게 한다.

## 주요 기여
1. 아나모픽 배율 + M3D 효과 통합 고속 High-NA EUV 이미징 모델
2. High-NA EUV용 소스-마스크 공동 최적화(SMO) 방법 개발
3. 아나모픽 광학계 OPC 보정 알고리즘 (비대칭 MRC 포함)
4. H-V 바이어스 감소 및 균형 패터닝 결과 달성

## Recipe/Process Flow 상세

### High-NA EUV 아나모픽 광학계 특성
```
기존 EUV (0.33NA):
  배율: 4× × 4× (등방성)
  마스크 패턴: 웨이퍼 대비 4× 확대
  쉐도잉: H/V 방향 유사

High-NA EUV (0.55NA):
  배율: 4× × 8× (비등방성 - 아나모픽)
  스캔 방향 (y): 8× 배율
  비스캔 방향 (x): 4× 배율
  마스크 NA 형상: 비등방 배율로 인한 타원형

영향:
  마스크 패턴 비대칭: x/y 방향 마스크 크기 다름
  OPC 모델: 비등방 광학 전달 함수 처리 필요
  MRC: x/y 방향 다른 마스크 제작 규칙
  쉐도잉: 비등방 입사각 분포 → 비대칭 쉐도잉 감소
```

### 아나모픽 OPC 모델 구성
```
전통 EUV OPC 모델 확장:
  기존: 등방성 TCC (Transmission Cross-Coefficient)
  High-NA: 비등방성 TCC → x/y 별도 처리

모델 구성 요소:
  1. 아나모픽 광학 전달 함수:
     - x: 4× 배율 광학 모델
     - y: 8× 배율 광학 모델
     - 편광: 비등방 입사로 인한 TM/TE 혼합

  2. M3D 효과 (High-NA 강화):
     - 비텔레센트리시티: 높은 NA → 더 큰 쉐도잉
     - 포커스 시프트: M3D로 인한 최적 포커스 변화
     - 마스크 스펙클: 두꺼운 흡수체 → 회절 복잡성

  3. 아나모픽 마스크 오차 팩터 (MEF):
     - x-MEF: 4× 배율에서의 마스크 오차 감도
     - y-MEF: 8× 배율에서의 마스크 오차 감도 (더 큰 오차 증폭)
     - 불균등 오차 증폭 → 비대칭 OPC 보정 필요

고속화:
  SOCS/BRA 분해: 아나모픽 TCC 저랭크 분해
  GPU 가속: CUDA FFT로 이미지 계산 가속
  대리 모델: 아나모픽 리소그래피 시뮬 CNN 근사
```

### SMO 알고리즘
```
목적 함수:
  min_{source, mask} EPE² + w_PW × (1/MEEF) + w_M3D × M3D_penalty
  제약: MRC(mask) ≥ 0, Source ∈ 허용 조명 공간

소스 최적화:
  자유형 픽셀: 조명 강도 맵 픽셀 단위 최적화
  SMO 반복: 소스 고정→마스크 최적화, 마스크 고정→소스 최적화

마스크 최적화 (아나모픽 OPC):
  ILT 기반: 비등방 광학 모델로 역방향 마스크 최적화
  아나모픽 MRC: x/y 방향 별도 마스크 제작 규칙 적용
  커비리니어: High-NA에서 최적 성능 위한 자유 형상 허용

수렴:
  교대 최적화: 소스/마스크 번갈아 최적화
  수렴 조건: EPE 변화 < 임계값
  반복: ~10-20 교대 반복
```

### 성능 결과
```
H-V 바이어스 감소:
  기존 EUV OPC: H/V 패턴 간 인쇄 차이 발생
  아나모픽 SMO: 비등방 쉐도잉 감소로 H-V 균형

DOF (Depth of Focus):
  아나모픽 SMO 최적화: DOF 향상
  High-NA DOF 제약 (NA 증가 → DOF 감소) 완화

고속 모델:
  아나모픽 High-NA 시뮬: GPU 가속으로 실용적 속도
  전체 칩 SMO: 합리적 TAT 내 완료 가능
```

## OPC 툴 구현 관련성
- **SKOPC High-NA 지원**: 아나모픽 광학 모델 추가로 High-NA EUV OPC 지원
- **SMO 확장**: NSGA-II SMO에 아나모픽 배율 효과 반영
- **M3D 모델**: High-NA 강화 M3D 효과 컴팩트 모델 통합
- **MRC 확장**: x/y 방향 비대칭 MRC 규칙 지원

## 참고문헌
- Opto-Electronic Advances (OEA), 2024
- DOI: https://doi.org/10.29026/oea.2024.230235
- 관련: High-NA EUV anamorphic optics (SPIE 2015, ASML/Zeiss)
- 관련: M3D effects in High-NA EUV (Erdmann et al., SPIE 2019)
- 관련: EUV stochastic OPC (Vaglio Pret et al., SPIE 2019)

## 태그
`Recipe`, `OEA`, `HighNA`, `EUV`, `Anamorphic`, `SMO`, `OPC`, `M3DEffects`, `MaskErrorFactor`, `ProcessWindow`, `ASML`, `2024`
