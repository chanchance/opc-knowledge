# High Accuracy OPC Electromagnetic Full-Chip Modeling for Curvilinear Mask OPC and ILT

## 메타데이터
- **저자**: Enas Sakr, Zac Levinson, Rob DeLancey, C. Jay Lee, Jinguang Li, Ryan Chen, Robert Iwanow, Delian Yang, Wolfgang Hoppe, Folarin Latinwo, Kevin Lucas, Peng Liu
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540N (10 April 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3013089

## 핵심 요약
곡선형 마스크 OPC 및 ILT를 위한 고정밀 전자기장(EM) 전체 칩 OPC 모델링 방법을 제시한다. 곡선형 마스크 패턴에서 발생하는 마스크 3D(M3D) 효과를 엄격한 전자기 계산으로 정확하게 모델링하여 OPC/ILT 정확도를 향상시킨다.

## 주요 기여
1. **곡선형 마스크 EM OPC 모델링**: 곡선형 패턴의 M3D 효과를 엄격한 EM 계산으로 정밀 모델링
2. **전체 칩 스케일 적용**: 단일 패턴 EM 계산을 전체 칩 OPC에 확장 적용
3. **ILT 정확도 향상**: EM 모델 기반 ILT로 곡선형 마스크 OPC 품질 향상
4. **산업 검증**: 실제 EUV 패터닝 데이터로 고정밀 EM OPC 모델 검증

## 알고리즘/수식
### EM 기반 곡선형 마스크 OPC 모델
```
기존 스칼라 OPC 모델:
  T_scalar(f): 마스크 형상만 고려 (M3D 무시)
  한계: 곡선형 패턴에서 M3D 효과 부정확

EM 기반 OPC 모델:
  T_EM(f) = RCWA(마스크 형상, 흡수층 재료, 두께)
  장점: 곡선형 패턴 포함 정확한 M3D 예측

전체 칩 EM 모델:
  Look-Up Table 방식:
    LUT[피치][방향][곡률] = T_EM 보정값
  또는:
    ML 대리 모델로 곡선형 패턴 EM 계산 가속화

OPC 정확도 비교:
  스칼라 OPC CD 오차: Δ_scalar
  EM OPC CD 오차: Δ_EM < Δ_scalar (곡선형 패턴에서 특히)
```

### 곡선형 마스크 M3D 특수 효과
```
곡선형 마스크 M3D 추가 효과:
  - 곡선 부분에서 입사각 변화 → M3D 효과 공간 변동
  - T-Y 접합부: 복잡한 EM 상호작용
  - 날카로운 코너: 전기장 집중 → M3D 강화

맨해튼 vs 곡선형 M3D 비교:
  맨해튼: 직각 코너 → 알려진 M3D 보정
  곡선형: 가변 곡률 → 동적 M3D 보정 필요
```

## OPC 툴 SMO 구현 관련성
- 곡선형 마스크 EM 모델: SKOPC 곡선형 OPC/ILT 모듈에서 EM 기반 M3D 모델 통합
- 전체 칩 EM LUT: 곡률/방향별 M3D 보정 LUT 설계
- SMO 정확도: EM M3D 모델로 SMO 비용 함수 계산 정확도 향상
- 고정밀 EUV OPC: 기존 스칼라 모델 한계를 EM 모델로 극복

## 태그
`OPC`, `EUV`, `electromagnetic`, `M3D`, `curvilinear`, `ILT`, `full_chip`, `RCWA`, `high_accuracy`, `DTCO`, `SPIE`, `2024`
