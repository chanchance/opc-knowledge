# Exploring the Crucial Role of Mask 3D-Induced Imaging Mechanisms in High- and Hyper-NA EUV Lithography

## 메타데이터
- **저자**: Andreas Erdmann, Gerardo Bottiglieri, Christian Schwemmer, Peter Evanschitzky, Tim Brunner, Eelco van Setten, Claire van Lare, Mark van de Kerkhof
- **소속**: Fraunhofer IISB / ASML
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 134240I (22 April 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3050542

## 핵심 요약
고NA(0.55NA) 및 하이퍼NA(>0.55NA) EUV 리소그래피에서 마스크 3D 효과가 이미징에 미치는 핵심 메커니즘을 근거리(near-field) 및 원거리(far-field) 회절광 분석을 통해 탐구한다. 방향 의존 이미지 비대칭성, 비텔레센트릭성, 피치 의존 최적 포커스, 이미지 블러 등 M3D 유발 효과를 분석한다.

## 주요 기여
1. **M3D 이미징 메커니즘 심층 분석**: 근거리/원거리 회절장 관점에서 M3D 효과 규명
2. **고NA/하이퍼NA 비교**: 0.55NA와 >0.55NA에서 M3D 효과 강도 비교
3. **방향 의존 비대칭**: H/V 패턴 간 이미지 비대칭성 정량화
4. **피치 의존 BFS**: 다양한 피치에서 M3D로 인한 최적 포커스 이동 분석

## 알고리즘/수식
### 고NA/하이퍼NA M3D 메커니즘
```
고NA EUV M3D 강화 원인:
  NA ↑ → 입사각 범위 ↑ → 마스크 옆면 회절 강화
  0.33NA: 입사각 범위 ≈ ±19°
  0.55NA: 입사각 범위 ≈ ±33°
  하이퍼NA: 입사각 범위 > ±33°

M3D 유발 이미징 효과:
  1. 방향 의존 비대칭: I_H(x) ≠ I_V(x) (H vs V 패턴)
  2. 비텔레센트릭성: 최적 포커스가 이미지 필드에서 기울어짐
  3. 피치 의존 BFS: ΔZ_best(pitch_A) ≠ ΔZ_best(pitch_B)
  4. 이미지 블러: M3D로 인한 추가적 이미지 번짐

근거리(near-field) vs 원거리(far-field):
  근거리: 마스크 표면 직근방의 전기장 분포
  → 흡수층 표면에서 에바네센트파 포함
  원거리: 마스크에서 멀리 전파된 회절 스펙트럼
  → OPC/SMO에서 사용하는 Hopkins TCC 계산의 입력
```

### SMO/OPC M3D 보정
```
고NA M3D 보정 전략:
  1. LUT 기반: pitch-orientation별 ΔCD_M3D LUT
  2. 저흡수층 (low-n/박막): M3D 효과 자체 감소
  3. 소스 최적화 (SMO): 방향 비대칭 완화 소스 형상

하이퍼NA 추가 과제:
  입사각 범위 더 넓어짐 → 기존 M3D 보정 부족
  → 더 정밀한 엄격 EM 계산 필요
```

## OPC 툴 SMO 구현 관련성
- 고NA/하이퍼NA M3D 모델: SKOPC 고NA 모듈에서 강화된 M3D 보정 필수
- 방향 비대칭 SMO: 소스 형상 최적화로 H/V 비대칭 완화
- 피치 의존 BFS: SMO에서 BFS 균일화를 비용 함수 항으로 추가
- 근거리/원거리 연계: 엄격 EM → Hopkins TCC 변환 파이프라인 설계

## 태그
`M3D`, `EUV`, `high_NA`, `hyper_NA`, `near_field`, `far_field`, `imaging_mechanism`, `BFS`, `asymmetry`, `SMO`, `OPC`, `Fraunhofer`, `ASML`, `SPIE`, `2025`
