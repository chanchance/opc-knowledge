# OPC Model Accuracy of Dry Resist Readiness for 0.55NA EUVL by Using Low-N Bright Field Mask

## 메타데이터
- **저자**: Dongbo Xu, Werner Gillijns, Jongchoel Park, Seo-Yeon Woo, Sungchul Oh, Youngsoo Kim, Jae-Hyun Kim, Jinwoo Park, Soo-Young Oh, Joost Bekaert, Geert Vandenberghe
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, Optical Microlithography XXXVIII, 134250X
- **DOI/URL**: https://doi.org/10.1117/12.3054162

## 핵심 요약
0.55NA EUV 리소그래피(High-NA EUV)와 건식 레지스트(dry resist) 결합 시 OPC 모델 정확도를 low-n 밝은 필드(bright field) 마스크 옵션과 함께 평가한다. imec N2 노드 28nm 피치 패턴을 대상으로, NXE:3400 스캐너 및 NXE:3600 High-NA 스캐너에서 dry resist OPC 모델 정확도를 검증한다. ML 기반 OPC 모델(N2R, N2E 등)을 활용하여 저-K1 EUV 패터닝에서의 dry resist 특성이 OPC 정확도에 미치는 영향을 분석한다.

## 주요 기여
1. **0.55NA + 건식 레지스트 OPC 평가**: High-NA EUV와 dry resist 결합 환경에서 OPC 모델 정확도 최초 체계적 평가
2. **Low-n 밝은 필드 마스크 OPC**: 낮은 굴절률 마스크 흡수체 옵션과 OPC 모델의 상호작용 분석
3. **28nm 피치 N2 노드 검증**: imec N2 기술 노드에서 OPC 모델 정확도 실증
4. **ML 기반 OPC 모델 비교**: N2R(resist only), N2E(etch included) ML 모델 정확도 비교
5. **Dry resist 특성 OPC 영향**: 높은 흡수율, 낮은 확산 등 dry resist 고유 특성의 OPC 파라미터 분리 처리

## Recipe/Flow 상세
- **0.55NA Dry Resist OPC 모델링 플로우**:
  1. **마스크 옵션 선정**:
     - Low-n bright field 마스크: 낮은 복소 굴절률 흡수체
     - High-NA 0.55NA 스캐너 특화 마스크 3D 효과 모델링
     - 마스크 shadowing, telecentricity 효과 포함
  2. **Dry Resist 특성 파악 및 모델링**:
     - 높은 EUV 흡수율 → 얕은 absorption depth
     - 낮은 분자 확산 → LWR 개선, CD 균일도 변화
     - 건식 현상(dry development) 특성 모델화
  3. **OPC 모델 캘리브레이션**:
     - NXE:3400(0.33NA) 및 NXE:3600(0.55NA) 데이터 수집
     - 28nm 피치 line/space, contact 패턴 SEM 측정
     - N2R: Resist 공정만 포함한 OPC 모델
     - N2E: Etch 공정까지 포함한 통합 OPC 모델
  4. **ML 기반 OPC 모델 학습**:
     - 레이아웃 특징 → ML 모델 → CD 예측
     - 물리 기반 모델 대비 정확도 향상 분석
  5. **검증 및 비교**:
     - 0.33NA vs. 0.55NA OPC 모델 정확도 비교
     - Dry resist vs. 습식 레지스트 OPC 파라미터 차이 분석
- **Low-N 마스크 특성**:
  - 낮은 굴절률(n) 흡수체 → 마스크 3D 효과 감소
  - Bright field 패턴: 기판이 밝음, 패턴이 어두움
  - High-NA EUV에서의 마스크 shadowing 최소화
- **적용 노드**: imec N2 (28nm 피치 BEOL)

## OPC 툴 구현 관련성
- High-NA EUV + dry resist 환경의 SKOPC 모델 확장 설계
- `high_na_dry_resist_opc.py`: 0.55NA 스캐너 + dry resist 통합 OPC 모델
- Low-n 마스크 흡수체 옵션별 OPC 파라미터 분리 처리
- ML 기반 N2R/N2E 모델을 SKOPC EUV 모델 캘리브레이션에 반영

## 태그
`HighNA`, `EUV`, `DryResist`, `0.55NA`, `OPC`, `LowNMask`, `BrightField`, `N2Node`, `28nm`, `MachineLearning`, `SPIE`, `2025`
