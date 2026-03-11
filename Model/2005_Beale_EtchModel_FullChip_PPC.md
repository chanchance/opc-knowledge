# Etch Modeling for Accurate Full-Chip Process Proximity Correction

## 메타데이터
- **저자**: Daniel F. Beale, James P. Shiely
- **연도**: 2005
- **게재지**: Proc. SPIE 5754, Optical Microlithography XVIII, 600815
- **DOI/URL**: https://doi.org/10.1117/12.600815

## 핵심 요약
전체 패터닝 공정의 에치 효과를 포함한 풀칩 공정 근접 보정(PPC: Process Proximity Correction)을 위한 에치 모델을 개발한다. CD 축소로 에치 공정 편향이 더 이상 작은 섭동으로 처리될 수 없어 OPC 모델에 명시적으로 포함해야 한다는 점을 강조한다.

## 주요 기여
1. 에치 공정 편향이 소규모 섭동 수준을 초과함을 정량적으로 규명
2. 풀칩 PPC(공정 근접 보정) 흐름에 에치 모델 통합 방법론 제시
3. 리소그래피 + 에치 결합 모델의 풀칩 교정 및 검증
4. 에치 효과를 별도 컴팩트 모델로 처리하는 선구적 접근
5. 다층 IC 레이어에서 에치 모델 적용성 검증

## 모델 수식/아키텍처
- **에치 컴팩트 모델**:
  - 1D 에치 바이어스: B_etch = f(CD, pitch, iso/dense 환경)
  - 2D 에치 근접 효과: 국소 패턴 밀도 함수
  - 리소그래피 + 에치 직렬 결합: CD_wafer = CD_resist + B_etch(CD_resist, env)
- PPC 흐름: 타겟 CD → 에치 보정 → 리소그래피 OPC 보정 → 마스크 CD
- 교정 데이터: 다양한 CD/피치의 웨이퍼 CD 측정값 (에치 후)

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [x] 하이브리드 (리소그래피 + 에치 결합 컴팩트 모델)

## OPC 툴 구현 관련성
- SKOPC 에치 근접 보정 모듈의 기초 참조 논문 (2005년 선구적 연구)
- 리소그래피-에치 직렬 모델 구조의 초기 구현 방법론
- `2014_Zavyalova_CombiningLithoEtch_OPC.md` 등 후속 연구의 기반
- 에치 모델을 OPC 흐름에 통합하는 표준적 접근 방식 확립

## 태그
`Model`, `Etch`, `OPC`, `PPC`, `FullChip`, `ProcessProximity`, `Calibration`, `SPIE`
