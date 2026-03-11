# Low-Contrast Photoresist Development Model for OPC Application at 10nm Node

## 메타데이터
- **저자**: Cheng-En Wu, David Wei, Charlie Zhang, Hua Song
- **연도**: 2015
- **게재지**: Proc. SPIE 9426, Optical Microlithography XXVIII, 94260N
- **DOI/URL**: https://doi.org/10.1117/12.2086044

## 핵심 요약
10nm 노드 이하에서 저대비(low-contrast) 공중 이미지에 대응하는 새로운 물리 컴팩트 레지스트 현상 모델을 제안한다. 다양한 설계 패턴에서 CD 예측 정확도와 모델 견고성을 향상시키는 확장 가능한 OPC 모델링 솔루션이다.

## 주요 기여
1. 저대비 공중 이미지 환경(10nm 노드)에서의 레지스트 현상 모델 개발
2. 기존 모델 대비 더 정확하고 확장 가능한(extendable) 물리 컴팩트 모델 제안
3. 다양한 설계 패턴에서 CD 예측 정확도 향상
4. 모델 견고성(robustness) 개선: 광학 조건 변화에 안정적 예측
5. 10nm 노드 이후 기술에도 적용 가능한 모델 확장성 검증

## 모델 수식/아키텍처
- **저대비 레지스트 모델**:
  - 고대비 가정 포기: 비선형 현상 속도 함수 R(I) 재정식화
  - 저대비 공중 이미지: I_max - I_min ≈ 작은 값 → 기존 임계값 모델 한계
  - 새 현상 모델: R(m) = R_max · (m/m_crit)^n (n 파라미터 저대비 조건 최적화)
- 탈보호 분율 모델: 낮은 공중 이미지 대비 조건에서 비선형 탈보호 반응
- 교정 데이터: ArF 193nm immersion, 10nm 노드 1D/2D 게이지 패턴

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC 레지스트 모델에서 10nm 이하 노드의 저대비 조건 처리 방법 참조
- 기존 CM1/CM0 모델의 저대비 환경 한계 극복을 위한 확장 방향
- EUV 저 k1 패터닝(저대비 공중 이미지 유사 환경)에도 원리 적용 가능
- `2006_Tyminski_CM0_ResistModel_OPC.md`, `2007_Zuniga_CM1_StandardProcessModel.md`의 후속 발전

## 태그
`Model`, `Resist`, `LowContrast`, `Development`, `10nm`, `OPC`, `PhysicalModel`, `SPIE`
