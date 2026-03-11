# Improving OPC Modeling Accuracy with Rigorous and Compact Modeling Deformation Effects in Photoresists

## 메타데이터
- **저자**: Folarin Latinwo, Bernd Kuechler, Rob DeLancey, Hyesook Hong, Delian Yang (Synopsys, Inc., USA/Germany)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 1249508
- **DOI/URL**: https://doi.org/10.1117/12.2660580

## 핵심 요약
NTD(Negative-Tone Development) 레지스트에서 발생하는 물리적 변형(deformation) 효과를 OPC 컴팩트 모델에 통합하여 OPC 모델링 정확도를 향상시킨 논문. 리고러스 시뮬레이션과 컴팩트 모델 두 가지 접근법으로 레지스트 변형 효과(수축, 팽윤 등)를 모델링하고, 이를 통해 CD 제어 정확도를 개선하였다.

## 주요 기여
1. **레지스트 변형 효과 모델링 체계**: NTD 레지스트의 화학적·물리적 물성(특히 변형/deformation)을 OPC 컴팩트 모델에 통합하는 방법론
2. **리고러스 + 컴팩트 이중 접근법**: 리고러스 시뮬레이션으로 물리 현상 파악 후 컴팩트 모델로 풀칩 수준 적용성 확보
3. **NTD 레지스트 특화 파라미터**: 기존 PTD(Positive-Tone Development) 레지스트 모델과 구분되는 NTD 고유 파라미터 도출
4. **OPC 정확도 개선 정량화**: 변형 효과 미포함 모델 대비 변형 효과 통합 모델의 EPE 개선량 측정
5. **CD 제어 요구 수준 충족**: 첨단 노드에서 요구되는 CD 제어 정확도 달성을 위한 레지스트 물성 모델링 확장

## 검증 방법론
- NTD 레지스트 패턴의 CD-SEM 측정 데이터와 리고러스/컴팩트 모델 예측값 비교
- 변형 효과 포함/미포함 OPC 모델의 캘리브레이션 잔차(RMSE) 비교
- 다양한 피처 크기 및 피치에서 모델 일반화 성능 검증
- 풀칩 OPC 플로우에서 컴팩트 변형 모델 적용 시 런타임 오버헤드 측정

## OPC 툴 구현 관련성
- SKOPC의 레지스트 모델(resist model) 컴포넌트에 NTD 레지스트 변형 파라미터 추가 시 참조
- `LithoEngine`에서 레지스트 모델 확장(변형 효과 포함) 구현의 이론적 기반
- `2019_Ho_OPC_model_building_EUV_lithography.md`와 연계하여 EUV 시대 레지스트 모델 요구사항 파악
- 레지스트 수축(shrinkage) 보정이 필요한 고해상도 패터닝에서 OPC 캘리브레이션 파이프라인 개선 근거

## 태그
`Verification`, `SPIE`, `OPC Model`, `Resist Model`, `NTD`, `Deformation`, `Calibration`, `CD Control`, `Compact Model`
