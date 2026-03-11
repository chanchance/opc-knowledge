# Improving OPC Modeling Accuracy with Rigorous and Compact Modeling Deformation Effects in Photoresists

## 메타데이터
- **저자**: Folarin Latinwo, Bernd Kuechler, Rob DeLancey, Hyesook Hong, Delian Yang
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 2660580
- **DOI/URL**: https://doi.org/10.1117/12.2660580

## 핵심 요약
NTD(Negative Tone Development) 레지스트 공정에서 레지스트 변형(deformation) 및 수축(shrinkage) 효과를 OPC 컴팩트 모델에 통합하여 모델 정확도를 향상시키는 방법을 제안한다. Synopsys에서 개발된 이 접근법은 물리적 레지스트 수축을 수식화한 탄성 컴팩트 모델(ECM)로 2D 패턴의 수축 유발 CD 편차를 정확하게 예측한다.

## 주요 기여
1. **레지스트 수축 OPC 모델 통합**: NTD 레지스트 수축/변형을 OPC 컴팩트 모델에 처음으로 체계적으로 반영
2. **탄성 컴팩트 모델(ECM)**: 임의 2D 레지스트 패턴의 탄성 변형 및 수축 유발 CD 편차 예측 모델
3. **리고러스-컴팩트 모델 연계**: 엄밀(rigorous) 시뮬레이션으로 컴팩트 모델 캘리브레이션 및 검증
4. **NTD 레지스트 공정 정확도 향상**: PEB(Post-Exposure-Bake) 및 현상 단계의 수축 효과 분리 모델링
5. **OPC 적용**: 수축 보정 OPC 모델로 실제 CD 정확도 향상

## Recipe/Flow 상세
- **레지스트 변형/수축 OPC 모델링 플로우**:
  1. **레지스트 수축 메커니즘 분석**:
     - PEB 단계: 열 유발 레지스트 수축 (가교 반응)
     - 현상 단계: 용매 침투 및 팽윤(swelling) 후 건조 수축
     - 2D 패턴 형상에 따른 차별적 수축 분포
  2. **엄밀(Rigorous) 시뮬레이션**:
     - 유한요소법(FEM)으로 레지스트 탄성 변형 계산
     - 수축 전후 레지스트 패턴 형상 변화 계산
     - 다양한 패턴 크기/형상에 대한 수축 특성 데이터 생성
  3. **탄성 컴팩트 모델(ECM) 구성**:
     - 엄밀 시뮬레이션 데이터로 컴팩트 모델 캘리브레이션
     - 입력: 광학 이미지, 패턴 형상 특징
     - 출력: 수축 유발 CD 편차 예측
     - 효율적인 full-chip 적용 가능한 컴팩트 모델
  4. **OPC 모델 통합**:
     - 기존 OPC 모델 파이프라인에 ECM 추가
     - 수축 보정 OPC: 수축 예상량 만큼 사전 보상
     - NTD 레지스트 공정에서 CD 오차 감소
  5. **검증**:
     - 다양한 패턴 환경에서 수축 보정 OPC 모델 정확도 측정
     - 기존 수축 미고려 OPC 대비 CD 잔차 비교
- **NTD 레지스트 특성**:
  - 음성 톤 현상: 노광된 영역이 잔존
  - 현상 후 수축: 트렌치 패턴에서 폭 감소
  - 2D 패턴(코너, T자 분기 등)에서 비균일 수축
- **적용 대상**: EUV NTD 레지스트 공정 OPC 모델, ArF NTD 공정

## OPC 툴 구현 관련성
- SKOPC 레지스트 모델에 수축 보정 컴팩트 모델 추가
- `resist_shrinkage_model.py`: 탄성 컴팩트 모델(ECM) 구현, OPC 파이프라인 통합
- NTD 레지스트 공정 레이어(EUV 메탈, ArF 이머젼 NTD) OPC 정확도 향상
- 리고러스 시뮬레이션 → 컴팩트 모델 캘리브레이션 워크플로우

## 태그
`OPC`, `ResistModel`, `Shrinkage`, `Deformation`, `NTD`, `CompactModel`, `ModelAccuracy`, `EUV`, `ArF`, `Synopsys`, `SPIE`, `2023`
