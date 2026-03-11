# High Accuracy OPC Modeling for New EUV Low-K1 Mask Technology Options

## 메타데이터
- **저자**: Enas Sakr, Rob DeLancey, Wolfgang Hoppe, Zac Levinson, Robert Iwanow, Ryan Chen, Delian Yang, Kevin Lucas
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950P
- **DOI/URL**: https://doi.org/10.1117/12.2658720
- **인용수**: 신규 논문 (Synopsys, SPIE Advanced Lithography 2023)

## 핵심 요약
EUV 리소그래피가 양산에 성공적으로 진입하면서 설계-리소그래피 공정 상호작용을 이해하기 위한 정밀 예측 능력이 중요해졌다. EUV는 DUV에서 존재하지 않는 추가적인 체계적(systematic) 및 스토캐스틱(stochastic) 변동 원인을 갖는다. 본 논문은 새로운 EUV 저k1 마스크 기술 옵션(Low-n 흡수체, 대안 마스크 스택 등)에 대해 고정밀 OPC 모델링 방법론을 제시한다.

## 주요 기여
1. EUV 고유 물리 현상(섀도잉, 플레어, 마스크 위상 효과, 마스크 스택 반사율, 마스크 흡수체 거동)을 포함한 고정밀 EUV OPC 모델 구축 방법론
2. 저k1 EUV 노드에서 새로운 마스크 기술 옵션(Low-n 흡수체 등)에 대한 OPC 모델 정확도 검증
3. EUV 스토캐스틱 및 체계적 변동을 OPC 모델에 통합하는 프레임워크
4. Synopsys Proteus 기반 EUV OPC 모델 빌딩 및 검증 플로우 실증

## 검증 방법론
- **EUV 특화 물리 모델 구성 요소**:
  - 마스크 위상 효과(Mask Topography / 3D mask effects): EMF(Electromagnetic Field) 시뮬레이션
  - 섀도잉(Shadowing): 경사 입사광에 의한 비대칭 이미지 왜곡 보정
  - 플레어(Flare): 산란광에 의한 장거리 배경 조도 보정
  - 마스크 스택 반사율: 저k1 마스크 흡수체 옵션별 반사율 변동 모델링
- **모델 정확도 평가**:
  - Simulated vs. Measured CD 비교 (RMSE, Max Error)
  - EPE 분포 통계 (평균, σ, 3σ)
  - 공정 윈도우(DOF, EL) 재현 정확도
- **검증 데이터**: NXE 계열 EUV 스캐너 실측 웨이퍼 CD 데이터

## 검증 지표
- EPE 허용 범위: EUV 저k1 노드 — 수 nm 이내 (노드별 스펙 적용)
- 시뮬레이터: Synopsys Proteus OPC 엔진 + EMF 마스크 모델
- 커버리지: 저k1 EUV 노드 로직 레이어 (라인/스페이스, 비아, 2D 패턴)

## OPC 툴 구현 관련성
- **EUV OPC 모델 빌딩 및 검증 모듈 구현의 핵심 참조**: `ModelingEngine`의 EUV 프로세스 모델 구성 시 포함해야 할 물리 효과(섀도잉, 플레어, 마스크 3D) 목록과 구현 방법 제공
- 마스크 3D 효과를 컴팩트 모델로 근사하는 Domain Decomposition 기법 적용 근거
- EUV OPC 검증 지표(CD RMSE, EPE 분포) 설정의 최신 실무 기준
- 저k1 EUV 노드 대응 OPC 정확도 향상 방향 — 고정밀 OPC와 검증의 연계 방법론

## 참고문헌
- SPIE DTCO and Computational Patterning II 2023, Vol. 12495
- Synopsys Proteus EUV OPC 관련 선행 연구 다수

## 태그
`Verification`, `SPIE`, `EUV`, `OPCModeling`, `LowK1`, `MaskTopography`, `Shadowing`, `Flare`, `Stochastic`, `ModelAccuracy`, `EMF`
