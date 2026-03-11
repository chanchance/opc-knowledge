# Deep Pattern Solution for Interpreting Systematic Defects

## 메타데이터
- **저자**: Min Chul Park, Yeji Kim, Bogyeong Kang, Namjae Kim, Byungseon Choi, Hyunjae Jang, Ji-Hye Lee, SeongRyeol Kim, Young-Gu Kim, Jae-Hyun Kang, Joong-Won Jeon, Dae Sin Kim
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250W
- **DOI/URL**: https://doi.org/10.1117/12.3050977

## 핵심 요약
체계적 결함(systematic defect)을 해석하기 위한 뉴럴 네트워크 기반의 seamless 프레임워크를 제안한다. 공정 변동 인자를 통합한 위험 패턴(Risk Pattern, RP) 탐지를 위한 신경망 예측 방법론과 구조적 시각화 기법을 개발하고, 사전에 정의되지 않은 숨겨진 설계 인자를 탐지하며 결함을 유발하는 취약 샘플을 식별하는 설명 방법론을 포함한다. 설계 규칙 강화와 수율 개선을 목표로 하는 삼성전자 양산 공정 기반 연구이다.

## 주요 기여
1. **신경망 기반 위험 패턴 탐지**: 공정 변동 인자를 통합한 NN 기반 RP 탐지 예측 방법론 개발
2. **구조적 시각화 기법**: 결함 패턴의 구조적 특징을 시각화하여 해석 가능한 AI 분석 도구 제공
3. **숨겨진 설계 인자 탐지**: 사전 정의되지 않은 레이아웃 특징에서 잠재 결함 인자 발굴
4. **취약 샘플 설명 방법론**: 결함 유발 취약 패턴에 대한 설명 가능한(explainable) 분석
5. **설계 규칙 강화**: 분석 결과를 기반으로 설계 규칙(Design Rule) 업데이트 및 강화

## Recipe/Flow 상세
- **딥러닝 기반 체계적 결함 해석 플로우**:
  1. **데이터 준비**:
     - 웨이퍼 검사(wafer inspection) 데이터 수집: 결함 위치 및 유형
     - 레이아웃 데이터: 결함 위치 주변 설계 패턴 추출
     - 공정 변동 데이터: CD, 오버레이 변동 정보
     - 결함/비결함 레이블링: 훈련 데이터셋 구성
  2. **신경망 모델 구성**:
     - 위험 패턴 탐지 NN: 레이아웃 패턴 특징 → 결함 확률 예측
     - 공정 변동 통합: 측정 변동 파라미터를 NN 입력에 통합
     - 구조적 시각화 레이어: 중요 패턴 특징 시각화 모듈
  3. **숨겨진 결함 인자 탐지**:
     - 비지도 학습: 사전 정의되지 않은 패턴 클러스터링
     - 이상 탐지: 통상적 패턴 분포에서 이탈한 취약 패턴 식별
     - 패턴 임베딩 공간 분석: 잠재 결함 인자의 기하학적 클러스터 해석
  4. **설명 가능한 AI 분석**:
     - Grad-CAM 또는 유사 설명 기법으로 결함 기여 영역 시각화
     - 취약 샘플 식별: 결함 확률 높은 레이아웃 패턴 분류 및 설명
     - 설계자/공정 엔지니어가 해석 가능한 결과 제공
  5. **설계 규칙 강화 적용**:
     - 분석된 결함 패턴을 기반으로 위험 패턴 목록 업데이트
     - 설계 규칙(DRC) 추가 또는 강화: 취약 패턴 제한
     - OPC/RET 레시피 피드백: 위험 패턴 대상 OPC 처리 강화
- **체계적 결함의 특성**:
  - 무작위 결함과 달리 특정 패턴/환경에서 반복적으로 발생
  - 설계 레이아웃 특징, 공정 변동, 광학 근접 효과의 복합 결과
  - 딥러닝으로 인간이 인식하기 어려운 복잡한 패턴-결함 상관관계 발굴
- **소속 기관**: SAMSUNG Electronics Co., Ltd. (대한민국)

## OPC 툴 구현 관련성
- SKOPC 위험 패턴 탐지 모듈에 딥러닝 기반 체계적 결함 분석 통합
- `systematic_defect_analyzer.py`: NN 기반 위험 패턴 탐지 및 시각화
- OPC 레시피 개선 피드백 루프: 탐지된 위험 패턴의 OPC 처리 강화
- 설계 규칙 업데이트 자동화: 체계적 결함 분석 결과 → DRC 규칙 업데이트

## 태그
`SystematicDefect`, `NeuralNetwork`, `RiskPattern`, `MachineLearning`, `DesignRule`, `ProcessVariation`, `ExplainableAI`, `DefectPrediction`, `OPC`, `Samsung`, `SPIE`, `2025`
