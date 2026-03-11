# Resist Shrinkage During Development: Rigorous Simulations and First Compact Model for OPC

## 메타데이터
- **저자**: Yuri Granik, Daman Khaira
- **연도**: 2020
- **게재지**: Proc. SPIE 11327, Optical Microlithography XXXIII
- **DOI/URL**: https://doi.org/10.1117/12.2552527

## 핵심 요약
레지스트 현상 중 발생하는 수축(shrinkage) 현상을 엄밀하게 시뮬레이션하고, OPC에 적용 가능한 최초의 컴팩트 모델인 Elastic Compact Model(ECM)을 제안한다. 임의의 2D 레지스트 패턴 벽면에 대한 수축 유도 바이어스를 물리적으로 포착한다.

## 주요 기여
1. **Elastic Compact Model (ECM)**: 레지스트 수축 효과를 OPC 흐름에 통합하기 위한 최초의 컴팩트 모델 정식화
2. 현상 공정 중 레지스트 수축의 엄밀한 시뮬레이션 프레임워크 개발
3. 2D 레지스트 패턴 벽면에 대한 수축 유도 CD 바이어스 정량화
4. OPC 및 ILT 응용을 위한 실용적 수축 보정 방법론 제시
5. 기존 NTD(Negative Tone Development) 레지스트의 수축 문제를 OPC 모델 정확도 관점에서 분석

## 모델 수식/아키텍처
- **Elastic Compact Model**: 탄성 역학 원리에 기반한 레지스트 수축 컴팩트 표현
- 수축 바이어스 B_shrink는 레지스트 벽 형상(aspect ratio) 및 재료 탄성 계수의 함수
- 2D 단면 프로파일에서 수축 유도 변위를 계산하여 CD 보정값 산출
- PEB(Post-Exposure Bake) 및 현상(development) 단계 모두에서 발생하는 수축 효과 모델링

## 모델 유형
- [ ] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- NTD 레지스트 공정에서 필수적인 수축 보정 모듈
- OPC 컴팩트 모델에 ECM 항 추가로 모델 정확도 개선 가능
- SKOPC의 ModelOPC / 레지스트 모델 교정 파이프라인에 직접 적용 가능
- ILT(Inverse Lithography Technology) 최적화와 결합 시 패턴 충실도 향상

## 태그
`Model`, `Resist`, `Shrinkage`, `Compact`, `NTD`, `OPC`, `ECM`, `SPIE`
