# OPC Accuracy Improvement Through Deep-Learning Based Etch Model

## 메타데이터
- **저자**: Weina Shi, Liang Zhu, Yuqian Chen, Jiao Huang, Jinze Wang, Qian Xie, Bilun Zhang, Yunfei Xi, Wenhao Pan, Yuanxia Zheng, Yongfa Fan, Jin Cheng, Yu Zhao, Leiwu Zheng
- **연도**: 2022
- **게재지**: Proc. SPIE 12056, Advanced Etch Technology and Process Integration for Nanopatterning XI, 1205607
- **DOI/URL**: https://doi.org/10.1117/12.2613926
- **인용수**: 신규 논문 (SPIE Advanced Etch Technology 2022)

## 핵심 요약
DUV 리소-에치(litho-etch) 케이스에서 딥러닝 기반 에치 모델(Newron etch model)을 사용한 전칩 OPC 보정 플로우를 시연한다. SEM 계측, 자동화 계측 소프트웨어, 딥러닝 에치 모델링을 결합하여 복잡한 에치 거동을 포착한다. Newron 에치 모델은 기존 term 기반 에치 모델 대비 모델 캘리브레이션 정확도를 테스트 패턴에서 50% 미만, 실제 칩 패턴에서 35% 미만으로 개선함을 입증한다.

## 주요 기여
1. 딥러닝 기반 Newron 에치 모델로 OPC 정확도 향상 — 기존 term 기반 대비 35~50% 오차 감소
2. SEM 계측 + 자동화 소프트웨어 + DL 에치 모델의 통합 전칩 OPC 플로우 구현
3. 복잡한 2D 에치 거동(로딩 효과, 이방성 에치 등)을 딥러닝으로 포착
4. DUV 리소-에치 케이스에서 실제 칩 레벨 검증

## 검증 방법론
- **딥러닝 에치 모델(Newron)**:
  - 입력: SEM 기반 레지스트 컨투어 + 주변 레이아웃 컨텍스트
  - 출력: 에치 후 CD(AEI: After Etch Inspection) 예측
  - 구조: CNN 기반 에치 바이어스 예측 신경망
- **OPC 플로우 통합**:
  - 1단계: 리소그래피 시뮬레이션으로 ADI 컨투어 예측
  - 2단계: DL 에치 모델로 AEI 컨투어 예측
  - 3단계: AEI 컨투어 기반 EPE 계산 및 마스크 보정
- **정확도 평가**:
  - 테스트 패턴: Newron < 50% 오차 (기존 모델 대비)
  - 실제 칩 패턴: Newron < 35% 오차 (기존 모델 대비)
  - 지표: RMS EPE, Max EPE (AEI 기준)
- **SEM 계측**: 자동화 CD-SEM 측정 소프트웨어로 대용량 게이지 수집

## 검증 지표
- EPE 허용 범위: AEI 기준 — DUV 노드 에치 후 CD 오차 수 nm 이내
- 시뮬레이터: Newron DL 에치 모델 + 리소그래피 시뮬레이터
- 커버리지: 테스트 패턴 + 실제 전칩 DUV 레이아웃

## OPC 툴 구현 관련성
- **에치 모델 통합 OPC 검증**: `ModelingEngine`에서 리소그래피 모델 후단에 에치 모델을 연결하여 AEI 기준 EPE를 계산하는 2단계 OPC 검증 파이프라인 설계에 직접 참조
- 딥러닝 에치 모델의 입출력 구조(레지스트 컨투어 → AEI 컨투어)는 `LithoEngine` 확장 모듈로 구현 가능
- AEI 기준 EPE 체크를 OPC 검증 지표로 추가하는 구현 근거 — ADI/AEI 이중 검증 플로우
- 에치 로딩·이방성 효과를 고려한 OPC 모델 정확도 향상으로 sign-off 신뢰도 제고

## 참고문헌
- SPIE Advanced Etch Technology and Process Integration for Nanopatterning XI 2022, Vol. 12056
- Newron DL 에치 모델 관련 선행 연구 (Accurate etch modeling with massive metrology and DL, SPIE 2020)

## 태그
`Verification`, `SPIE`, `EtchModel`, `DeepLearning`, `OPCAccuracy`, `AEI`, `ADI`, `Contour`, `EtchBias`, `FullChip`, `DUV`
