# Wafer Hotspot Prevention Using Etch Aware OPC Correction

## 메타데이터
- **저자**: Ayman Hamouda, Dave Power, Mohamed Salama, Ao Chen
- **연도**: 2016
- **게재지**: Proc. SPIE 9781, Design-Process-Technology Co-optimization for Manufacturability X, 978115
- **DOI/URL**: https://doi.org/10.1117/12.2220778

## 핵심 요약
에치 인식(etch-aware) OPC 보정을 사용하여 웨이퍼 핫스팟을 예방하는 방법을 제안한다. 레지스트와 에치 응답을 결합한 집약 모델(lumped model)을 교정·검증하고, 다중 패터닝에서 노광 간 핫스팟과 에치 후 결함을 보다 정확하게 보정한다.

## 주요 기여
1. 에치 인식 동시 다중 패터닝 OPC 방법론 제안
2. 레지스트 + 에치 응답 결합 집약 모델(lumped model) 교정 및 검증
3. 노광 간(inter-exposure) 핫스팟 예측 및 보정
4. 에치 후 결함의 보다 정확한 OPC 보정 (기존 다중 패터닝 OPC 대비)
5. 에치 공정을 OPC 흐름에 통합하는 실용적 풀칩 접근법

## 모델 수식/아키텍처
- **결합 집약 모델(Lumped Model)**:
  - CD_wafer = f(CD_resist, CD_etch_bias)
  - CD_etch_bias = g(CD_resist, pitch, local_density)
  - 교정: CD_wafer 측정값으로 전체 모델 파라미터 동시 최적화
- 다중 패터닝 OPC: LELE/SADP 분해 → 각 노광의 OPC + 에치 보정
- 핫스팟 분류: 에치 후 CD 분포 → 스펙 위반 패턴 자동 식별
- 에치 보정: 핫스팟 패턴의 마스크 바이어스 추가 조정

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [x] 하이브리드 (리소그래피 + 에치 결합 모델)

## OPC 툴 구현 관련성
- SKOPC 에치 인식 OPC 모듈 및 핫스팟 방지 기능 구현 참조
- 다중 패터닝(LELE, SADP) 흐름에서 에치 보정 통합 방법
- 레지스트-에치 결합 모델의 실용적 교정 방법론
- `2014_Zavyalova_CombiningLithoEtch_OPC.md`의 방법론을 핫스팟 방지에 적용한 사례

## 태그
`Model`, `Etch`, `OPC`, `Hotspot`, `MultiPatterning`, `LumpedModel`, `EtchAware`, `DTCO`, `SPIE`
