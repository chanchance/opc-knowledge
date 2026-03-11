# Improving OPC Model Accuracy of Dry Resist for Low K1 EUV Patterning

## 메타데이터
- **저자**: Dongbo Xu, Werner Gillijns, Joost Bekaert, Geert Vandenberghe, et al.
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, Optical Microlithography XXXVII, 129540X
- **DOI/URL**: https://doi.org/10.1117/12.3010xxx

## 핵심 요약
저-K1 EUV 패터닝 환경에서 건식(dry) 레지스트의 OPC 모델 정확도를 향상시키는 방법을 연구한다. 기존 습식 레지스트 기반 OPC 모델 프레임워크를 dry resist의 독특한 물리적·화학적 특성에 맞게 수정하고, 저-K1 조건(k1 < 0.3)에서 OPC 모델 정확도를 극대화하는 캘리브레이션 전략을 제시한다.

## 주요 기여
1. **Dry Resist OPC 모델 프레임워크 개선**: 기존 습식 레지스트 모델 대비 dry resist 고유 특성 반영
2. **저-K1 EUV 조건 최적화**: k1 < 0.3 초고해상도 영역에서의 OPC 정확도 향상
3. **Dry Resist 캘리브레이션 전략**: 최소 측정 데이터로 높은 모델 정확도 달성하는 캘리브레이션 플로우
4. **습식 vs. 건식 레지스트 OPC 비교**: 두 레지스트 시스템의 OPC 파라미터 및 모델 구조 차이 체계적 분석
5. **EUV 공정 창 예측**: Dry resist OPC 모델의 공정 창(Process Window) 예측 정확도 검증

## Recipe/Flow 상세
- **저-K1 EUV Dry Resist OPC 모델 개선 플로우**:
  1. **Dry Resist 물리 특성 분석**:
     - 높은 EUV 흡수율 (기존 습식 대비 2~3배)
     - 낮은 분자 확산 길이 → 더 sharp한 Image Log Slope (ILS) 의존성
     - 건식 현상(vapor-phase development) 메커니즘
     - 확산 없는 화학증폭(CAR-less) 반응
  2. **OPC 모델 구조 수정**:
     - 광학 모델: EUV shadowing, flare, across-slit CD 변화 포함
     - 레지스트 모델: 낮은 확산 계수 반영 (확산 커널 폭 축소)
     - 현상 모델: 건식 현상 속도 모델 수정
  3. **캘리브레이션 데이터 수집**:
     - 저-K1 조건(k1 = 0.25~0.30) 패턴 SEM 측정
     - Line/space, contact/via, 2D 패턴 다양하게 포함
     - Focus-dose matrix 측정 (공정 창 캘리브레이션)
  4. **모델 피팅 및 검증**:
     - Dry resist 특화 파라미터 최적화
     - 교차 검증: 캘리브레이션 패턴 외 새 패턴에서 모델 예측 정확도 측정
  5. **OPC 적용 및 웨이퍼 검증**:
     - 개선된 dry resist 모델로 저-K1 EUV 레이아웃 OPC 수행
     - 프린팅 결과와 시뮬레이션 비교
- **저-K1 EUV 특수 고려사항**:
  - 높은 NILS(Normalized Image Log Slope) 요구
  - Stochastic 노이즈 영향 증가 → 모델의 확률론적 성분 필요
  - 마스크 3D 효과(M3D) 더욱 중요해짐
- **Dry Resist 모델 장점**: 낮은 확산으로 LWR 개선 → OPC 모델 단순화 가능

## OPC 툴 구현 관련성
- SKOPC EUV 레지스트 모델에서 dry resist 옵션 추가
- `dry_resist_model.py`: 낮은 확산 계수, 건식 현상 속도 모델 구현
- 저-K1 EUV OPC 레시피에서 dry resist 파라미터 별도 관리
- 캘리브레이션 플로우: dry resist 특화 gauge 패턴 선택 기준

## 태그
`DryResist`, `EUV`, `OPC`, `LowK1`, `ModelCalibration`, `Resist`, `BEOL`, `SPIE`, `2024`
