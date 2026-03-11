# EUV OPC Modeling and Correction Requirements

## 메타데이터
- **저자**: (SPIE 9048 - 2014 SPIE Advanced Lithography)
- **연도**: 2014
- **게재지**: Proc. SPIE 9048, Extreme Ultraviolet (EUV) Lithography V
- **DOI/URL**: https://doi.org/10.1117/12.2046341
- **인용수**: ~35

## 핵심 요약
EUV 리소그래피를 위한 OPC 모델링 및 보정의 고유한 요구사항을 체계적으로 분석한다. EUV의 반사형 마스크, 마스크 3D 효과, 플레어(flare), off-axis 조명에 의한 비대칭 효과 등 ArF와 본질적으로 다른 물리 현상이 OPC 모델과 보정 흐름에 미치는 영향을 규명하고, 10nm 노드 EUV OPC 모델링의 요구사항과 해결 방향을 제시한다.

## 주요 기여
1. EUV 리소그래피 고유 효과와 OPC 모델 요구사항의 체계적 분류
2. 마스크 3D 효과가 OPC 정확도에 미치는 영향 정량화
3. EUV 플레어 보정을 위한 OPC 통합 방법론
4. 10nm 노드 EUV OPC 모델 구축 실증

## Recipe/Process Flow 상세

### EUV 리소그래피와 ArF의 OPC 모델 차이
```
ArF 리소그래피 (193nm, 투과형 마스크):
  - 마스크: 크롬/MoSi 흡수체, 투과형
  - 조명: 수직 입사 (텔레센트릭)
  - Kirchhoff 근사 적용 가능 (마스크 두께 << λ)
  - OPC 모델: 광학 + 레지스트 모델로 충분

EUV 리소그래피 (13.5nm, 반사형 마스크):
  - 마스크: Mo/Si 다층 반사경 + 흡수체, 반사형
  - 조명: 6도 경사 입사 (non-telecentic)
  - 마스크 두께 ≈ λ → Kirchhoff 근사 부적절
  → 엄밀한 전자기(EM) 시뮬레이션 필요

EUV OPC 모델 추가 요인:
  1. 마스크 3D 효과:
     - 흡수체 두께로 인한 위상 왜곡
     - Shadowing 효과 (방향 의존 CD 변화)
  2. EUV 플레어 (Flare):
     - 광학계의 표면 거칠기에 의한 산란광
     - 배경 노광 강도 증가 → CD bias
  3. Non-telecentricity:
     - 6도 경사 조명 → 수평/수직 방향 패턴 비대칭
  4. 반사형 마스크 수차:
     - 마스크 형상 의존 위상 오차
```

### EUV OPC 모델 구축 방법론
```
1단계: 광학 모델
  a) 도메인 분해(Domain Decomposition) 기반 엄밀 마스크 모델
     - 3D 마스크 EM 시뮬레이션 (RCWA 또는 FDTD)
     - 주기 패턴: 엄밀 솔루션
     - 비주기 패턴: 로컬 주기화 근사
  b) Flare 모델:
     - 공간 주파수 의존 PSF로 플레어 맵 기술
     - 플레어 보정 타겟 CD 조정
  c) 비텔레센트릭 보정:
     - Off-axis 조명에 의한 마스크 이미지 시프팅 보상
     - H/V 방향 분리 보정

2단계: 레지스트 모델
  - EUV 레지스트의 광자 수 제한 노이즈 (stochastic effect)
  - 확률론적 레지스트 모델 또는 컴팩트 모델 조정
  - 선량 의존 레지스트 파라미터 추출

3단계: 캘리브레이션
  - EUV 전용 테스트 패턴 설계
  - H/V 방향 분리 측정 (비대칭 효과 분리)
  - Flare 레벨별 CD 측정
  - 모델 파라미터 최적화
```

### 10nm 노드 EUV OPC 적용 결과
```
마스크 3D 보정 효과:
  H/V 방향 CD 바이어스 차이: 3D 모델로 감소
  라인-엔드 단축 예측: 개선

Flare 보정 효과:
  배경 노광 보상 후 CD uniformity 향상
  Dense/isolated 간 CD 차이 감소

모델 정확도 (RMS EPE):
  표준 Kirchhoff 모델 대비 3D 모델 우세
  특히 2D 패턴, 코너 영역에서 차이 두드러짐
```

## OPC 툴 구현 관련성
- **SKOPC EUV 모드**: `skopc/core/litho_engine.py`에 EUV용 반사형 마스크 모델, flare 보정, 비텔레센트릭 효과 추가
- **마스크 3D 효과**: 방향 의존 CD 바이어스 보정 테이블 또는 EM 시뮬 인터페이스
- **Flare 보정**: 공간 flare 맵 계산 후 OPC 타겟 CD 보정 전처리
- **레시피 파라미터**: `recipes/example_euv.yaml`에 EUV 전용 모델 파라미터(flare_level, m3d_correction) 추가

## 참고문헌
- Proc. SPIE 9048, Extreme Ultraviolet (EUV) Lithography V (2014)
- 관련: Mask 3D effects and compensation for high NA EUV lithography (SPIE 8679, 2013)
- 관련: Advanced OPC Mask-3D and Resist-3D modeling (SPIE 9052, 2014)
- 관련: SRAF requirements and impact on EUV lithography (SPIE 10583, 2018)

## 태그
`Recipe`, `SPIE`, `EUVLithography`, `OPC-Modeling`, `Mask3DEffect`, `Flare`, `NonTelecentricity`, `EUV-OPC`, `10nm`, `EM-Simulation`, `2014`
