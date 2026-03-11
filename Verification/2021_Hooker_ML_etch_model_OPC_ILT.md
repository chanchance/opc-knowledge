# Using Machine Learning Etch Models in OPC and ILT Correction

## 메타데이터
- **저자**: Kevin Hooker, Lena Zavyalova, Shuo Huang, Li-Jin Chen
- **연도**: 2021
- **게재지**: Proc. SPIE 11614, Design-Process-Technology Co-optimization XV, 116140B
- **DOI/URL**: https://doi.org/10.1117/12.2587225
- **인용수**: 다수 (Synopsys, SPIE DTCO 2021)

## 핵심 요약
OPC 및 ILT 보정에서 에치 효과를 정확히 고려하는 것이 점점 더 중요해지고 있다. 기존 마스크 합성 플로우는 규칙 기반 에치 근접 효과 접근법을 사용해왔으나 정확도 한계로 모델 기반 에치 마스크 보정의 광범위 채택이 제한되었다. 본 논문은 ML 에치 모델을 활용하여 TAT(Turn-Around Time) 희생 없이 모델 정확도를 향상시키고, ML 에치 모델을 사용하는 ILT 기반 에치 보정 방법을 시연한다.

## 주요 기여
1. ML 에치 모델의 OPC·ILT 통합 — 정확도 향상과 TAT 유지의 균형 달성
2. ILT 기반 에치 보정: ML 에치 모델이 ADI 타겟 컨투어를 출력하고 OPC/ILT가 이를 마스크 보정 타겟으로 사용
3. ML 에치 모델이 기존 term 기반 모델의 정확도 한계를 극복함을 실증
4. 에치 모델 기반 AEI 컨투어 예측을 OPC 검증 플로우에 통합하는 방법론 제시

## 검증 방법론
- **ML 에치 모델 구조**:
  - 입력: ADI(리소그래피 후) 컨투어 + 주변 레이아웃 컨텍스트
  - 출력: AEI(에치 후) CD 바이어스 예측
  - 모델: ML 회귀 모델 (신경망 또는 앙상블 기반)
- **ILT 기반 에치 보정 플로우**:
  1. ML 에치 모델로 ADI → AEI 컨투어 변환
  2. AEI 컨투어를 ILT/OPC의 보정 타겟으로 설정
  3. ILT/OPC가 AEI 타겟 기준으로 마스크 패턴 최적화
- **정확도 평가**:
  - 기존 term 기반 에치 모델 vs. ML 에치 모델 AEI CD 예측 오차 비교
  - OPC/ILT 수렴 후 AEI EPE 분포
- **TAT 평가**: ML 모델 런타임 vs. 기존 모델 런타임 비교

## 검증 지표
- EPE 허용 범위: AEI 기준 — 선단 노드 에치 후 CD 스펙
- 시뮬레이터: Synopsys ML 에치 모델 + Proteus OPC/ILT 엔진
- 커버리지: OPC·ILT 보정 대상 레이어 (라인/스페이스, 비아, 컨택트)

## OPC 툴 구현 관련성
- **에치 모델 통합 OPC/ILT 검증 플로우 설계**: `ModelingEngine`에서 ML 에치 모델을 리소그래피 모델과 직렬 연결하여 AEI 기준 EPE 검증을 수행하는 2단계 파이프라인 구현에 직접 참조
- ILT 에치 보정 플로우의 ADI 타겟 컨투어 생성 알고리즘 — `ModelingEngine`의 OPC 타겟 설정 모듈 구현에 활용
- ML 에치 모델의 빠른 추론 속도는 전칩 에치 보정 검증의 TAT 유지에 핵심 — 구현 효율성 기준 제공
- OPC 검증 시 ADI(리소그래피) 기준과 AEI(에치) 기준 이중 체크를 추가하는 구현 방향 제시

## 참고문헌
- SPIE Design-Process-Technology Co-optimization XV 2021, Vol. 11614
- Synopsys Proteus OPC/ILT + ML 에치 모델 관련 연구

## 태그
`Verification`, `SPIE`, `EtchModel`, `MachineLearning`, `OPC`, `ILT`, `ADI`, `AEI`, `EtchBias`, `AEIContour`, `TAT`, `FullChip`
