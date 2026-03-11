# Process Window OPC Verification: Dry versus Immersion Lithography for the 65nm Node

## 메타데이터
- **저자**: Amandine Borjon, Jerome Belledent, Yorick Trouiller, Kevin Lucas, Christophe Couderc, Frank Sundermann, Jean-Christophe Urbani, Yves Rody, Christian Gardin, Frank Foussadier, Patrick Schiavone
- **연도**: 2006
- **게재지**: Proc. SPIE 6154, Optical Microlithography XIX, 61544D
- **DOI/URL**: https://doi.org/10.1117/12.657056

## 핵심 요약
65nm 기술 노드에서 건식(Dry) 리소그래피와 침지(Immersion) 리소그래피의 공정 윈도우 OPC 검증을 비교한 논문. 건식 리소그래피용으로 확립된 컴팩트 광학 모델 기반 공정 윈도우 OPC 검증 방법론이 침지 리소그래피에도 유효한지를 Poly 레이어에서 실증적으로 검증하고, 두 리소그래피 방식 간의 공정 윈도우 모델 예측 정확도를 비교하였다.

## 주요 기여
1. **Dry vs. Immersion OPC 검증 모델 비교**: 건식/침지 리소그래피 환경에서 각각 캘리브레이션된 컴팩트 공정 윈도우 모델의 예측 정확도 비교
2. **침지 리소그래피 OPC 검증 검증(validation)**: 건식 리소그래피에서 확립된 공정 윈도우 OPC 검증 방법론의 침지 리소그래피 적용 타당성 실증
3. **공정 윈도우 한계 조건 모델 캘리브레이션**: 공정 윈도우 경계 조건(포커스/도즈 한계)에서의 실험 데이터로 컴팩트 모델 캘리브레이션 방법 제시
4. **OPC 후 프린터빌리티 예측**: OPC 결과물에 대해 공정 변동 전 범위에서 잠재 인쇄 실패를 예측하는 검증 플로우
5. **Poly 레이어 65nm 노드 실증**: 실제 65nm Poly 레이어에서 두 리소그래피 방식의 검증 결과 정량 비교

## 검증 방법론
- 건식/침지 리소그래피 공정 윈도우 경계 실험 데이터로 각각 컴팩트 모델 캘리브레이션
- 포커스-도즈 매트릭스(FEM)에서 OPC 검증 모델 예측과 실측 CD 비교
- 공정 윈도우 내 인쇄 실패 예측 정확도(false positive/negative) 비교
- Dry 대비 Immersion의 공정 윈도우 크기 및 OPC 검증 신뢰도 비교 정량화

## OPC 툴 구현 관련성
- SKOPC의 공정 윈도우 OPC 검증 모듈에서 침지/건식 리소그래피 모델 차이를 처리하는 설계 근거
- `2007_Lee_LRC_process_window_error_detection.md`(기수집)의 LRC 기반 공정 윈도우 검증과 함께 읽어야 할 핵심 선행 논문
- SKOPC `recipes/example_arfimm.yaml`(ArF 침지) 공정의 공정 윈도우 OPC 검증 파라미터 설계 기준
- 침지 리소그래피 특유의 공정 윈도우 축소 효과를 OPC 검증 기준값(threshold) 설정에 반영할 근거

## 태그
`Verification`, `SPIE`, `Process Window`, `OPC`, `Immersion Lithography`, `Dry Lithography`, `65nm`, `Compact Model`, `Poly Layer`
