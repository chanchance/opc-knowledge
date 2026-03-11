# Enabling Source and Mask Optimization by a Dynamic Aberration Imaging Model Across the Full Exposure Field

## 메타데이터
- **저자**: (SPIE 13423 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13423, Optical Microlithography XXXVIII, 134230U (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3052955

## 핵심 요약
전체 노출 필드(full exposure field)에 걸쳐 동적 수차(dynamic aberration) 이미징 모델을 사용하여 소스-마스크 최적화를 가능하게 하는 방법을 제안한다. 이미징 영향을 보상하기 위한 SMO 방법을 제안하여, 필드 전체에서 균일한 리소그래피 성능을 달성한다.

## 주요 기여
1. **동적 수차 이미징 모델**: 필드 위치 의존 수차를 포함한 전체 필드 이미징 모델
2. **전체 필드 SMO**: 단일 클립이 아닌 전체 노출 필드에 걸친 SMO 수행
3. **수차 보상 SMO**: 동적 수차 영향을 보상하는 SMO 방법론
4. **필드 균일성 향상**: 필드 전체에서 일관된 이미징 성능 달성

## 알고리즘/수식
### 동적 수차 이미징 모델
```
전체 필드 이미징:
I(x, y_field) = I_litho(x, J, M, W(y_field))

여기서:
- (x): 웨이퍼 위치
- y_field: 필드 내 위치 (슬릿 방향)
- J: 소스 조명
- M: 마스크 패턴
- W(y_field): 필드 위치 의존 Zernike 수차 계수

동적 수차 (필드 의존):
W(y_field) = Σ_k c_k(y_field) · Z_k(ρ, θ)
  c_k(y_field): 필드 위치에 따른 k번째 Zernike 계수 변화
```

### 수차 보상 SMO
```
비용 함수 (전체 필드 평균):
Cost = Σ_{y_f} w(y_f) · ||CD(x, J, M, W(y_f)) - CD_target||²

최적화:
  min_{J, M} Cost
  subject to: 모든 필드 위치에서 EPE ≤ EPE_budget

수차 보상 전략:
  - 소스 형상 J를 필드 평균 수차에 강건하게 최적화
  - 마스크 패턴 M에 필드 의존 수차 보정 항 추가
```

## OPC 툴 SMO 구현 관련성
- 전체 필드 SMO: 단일 클립 기반 SMO의 한계 극복 방향
- 동적 수차 모델: SMO 비용 함수에 필드 의존 수차 항 통합 필요
- 필드 균일성 목표: SMO 비용 함수에 필드 위치 가중 평균 추가
- SKOPC SMO 모듈에서 필드 전체 수차 맵 입력 지원 아키텍처 참조

## 태그
`SMO`, `dynamic_aberration`, `full_field`, `Zernike`, `field_uniformity`, `aberration_compensation`, `SPIE`
