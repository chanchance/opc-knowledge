# Physical Resist Models and Their Calibration: Their Readiness for Accurate EUV Lithography Simulation

## 메타데이터
- **저자**: U. K. Klostermann, T. Mülders, T. Schmöller, G. F. Lorusso, E. Hendrickx
- **연도**: 2010
- **게재지**: Proc. SPIE 7636, Optical Microlithography XXIII, 763619
- **DOI/URL**: https://doi.org/10.1117/12.846549

## 핵심 요약
물리 기반 레지스트 모델의 교정 방법론과 EUV 리소그래피 시뮬레이션에 대한 준비 상태를 평가한다. 32~40nm 선폭의 H/V 방향 패턴과 다양한 피치에 대한 공정 윈도우 데이터로 모델을 교정하고, EUV 시뮬레이션 정확도 예측 능력을 검증한다.

## 주요 기여
1. 물리 기반 레지스트 모델(화학 증폭 레지스트 물리 반응 포함)의 EUV 교정 방법론
2. 32/36/40nm 선폭, H/V 방향, 고밀도/저밀도 피치 조합으로 공정 윈도우 교정
3. 교정된 물리 모델의 EUV 리소그래피 정확도 예측 능력 평가
4. ArF 물리 모델에서 EUV 모델로의 전환 가능성 및 필요 수정 사항 분석
5. 물리 모델 교정의 한계와 컴팩트 모델 대비 장단점 비교

## 모델 수식/아키텍처
- **화학 증폭 레지스트(CAR) 물리 모델**:
  1. 노광: 공중 이미지 → 산(acid) 생성 분포 A(x,y)
  2. PEB: 산 확산 방정식 ∂A/∂t = D∇²A (확산 계수 D 교정)
  3. 현상: 탈보호 분율 → 현상 속도 함수 R(m) → CD
- 교정 파라미터: 확산 길이 σ_PEB, 현상 속도 대비 n, 임계 탈보호 분율 m_crit
- EUV 특수성: 짧은 파장, 높은 광자 에너지, 낮은 광자 수 → 확률론적 효과 증가

## 모델 유형
- [ ] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC EUV 레지스트 모델 구현 시 물리 기반 접근의 기준 논문
- ArF → EUV 레지스트 모델 전환 전략 이해에 유용
- 컴팩트 모델(CM1/CM0)의 물리적 의미를 물리 모델 관점에서 해석 가능
- `2009_Adam_CalibrationPhysicalResistModels.md`와 함께 물리 레지스트 모델 교정 핵심 시리즈

## 태그
`Model`, `Resist`, `Physical`, `EUV`, `Calibration`, `CAR`, `AcidDiffusion`, `ProcessWindow`, `SPIE`
