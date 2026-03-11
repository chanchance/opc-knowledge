# Guided Random Synthetic Layout Generation and Machine-Learning Based Defect Prediction for Leading Edge Technology Node Development

## 메타데이터
- **저자**: Geng Han, Mohamed Talbi, Monirul Islam, Rajiv Sejpal, Brad Austin, Rebekah Sheraw (IBM Thomas J. Watson Research Center), Joe Kwan, Sophie Rissberger, Qian Xie, Alex Dolgonos, Bennett Smith, Shibing Wang, Xuefeng Zeng, Yuyang Sun (Siemens EDA)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 1342509
- **DOI/URL**: https://doi.org/10.1117/12.3051134

## 핵심 요약
합성 레이아웃(synthetic layout) 생성과 기계학습 기반 결함 예측을 결합하여 첨단 기술 노드 개발을 가속화하는 플로우를 제안한다. 유도된 무작위 합성 레이아웃 생성으로 훈련 데이터를 대량 확보하고, ML 기반 결함 예측 모델을 고정밀로 캘리브레이션하여 M1 핀칭(pinching), 라인 끝 풀백(line-end pullback) 등 특정 결함 모드 탐지 정확도를 향상시킨다. IBM-Siemens EDA 공동 연구로 합성 레이아웃+ML 핫스팟 탐지 통합 → 표적 검사 전략 가속화.

## 주요 기여
1. **합성 레이아웃 생성 플로우**: 유도된 무작위(guided random) 방식으로 다양한 패턴의 합성 레이아웃 대량 생성
2. **ML 결함 예측 모델 고정밀 캘리브레이션**: M1 핀칭, 라인 끝 풀백 등 특정 결함 모드 탐지 ML 모델 개발
3. **합성+ML 핫스팟 탐지 통합**: 합성 레이아웃과 ML 기반 핫스팟 탐지를 통합하여 표적 검사 전략 수립
4. **신기술 노드 개발 가속화**: 실제 양산 레이아웃 없이 합성 데이터로 신규 노드 OPC/결함 예측 모델 조기 개발
5. **IBM-Siemens 협력**: 산업계 연구기관과 EDA 툴 제공사 공동 방법론 개발

## Recipe/Flow 상세
- **합성 레이아웃 + ML 결함 예측 통합 플로우**:
  1. **유도된 무작위 합성 레이아웃 생성**:
     - 기술 노드 설계 규칙(DRC)을 따르는 무작위 레이아웃 자동 생성
     - 유도(guided) 알고리즘: 특정 피치, 끝-간격(tip-to-tip), 고립도 등 결함 유발 패턴 강화
     - 실제 회로 레이아웃 통계 특성을 반영한 합성 데이터 생성
     - 대량 레이아웃 생성: 소수 실제 데이터 부족 극복
  2. **OPC 시뮬레이션 및 결함 레이블링**:
     - 생성된 합성 레이아웃에 OPC 적용: 리소그래피 시뮬레이션
     - 결함 후보 탐지: M1 핀칭, 라인 끝 풀백, CD 이상 등
     - 결함/비결함 레이블링으로 ML 훈련 데이터셋 구성
  3. **ML 결함 예측 모델 개발 및 캘리브레이션**:
     - 특징 추출: 레이아웃 패턴의 기하학적, 광학적 특징 벡터화
     - ML 모델 학습: 훈련 데이터셋으로 결함 예측 모델 훈련
     - 모델 캘리브레이션: 실제 웨이퍼 데이터로 예측 정확도 보정
     - 특정 결함 모드별 전용 모델: M1 핀칭 전용, 라인 끝 풀백 전용 등
  4. **합성+ML 핫스팟 탐지 통합**:
     - 합성 레이아웃 → ML 모델 → 핫스팟 후보 탐지
     - 핫스팟 위치 집중 검사(targeted inspection) 계획 수립
     - 검사 비용 절감: 전수 검사 → 핫스팟 중심 표적 검사
  5. **신기술 노드 개발 적용**:
     - 실제 제품 레이아웃 없이 합성 데이터로 OPC 모델 조기 개발
     - 설계 규칙 검증 및 개선: ML 탐지 결과 → DRC 업데이트
     - 테이프아웃 전 결함 위험 패턴 사전 식별
- **합성 레이아웃 생성 장점**:
  - IP 보안 없이 대량 훈련 데이터 확보
  - 실제 결함이 적은 신규 노드에서 불균형 데이터 문제 극복
  - 특정 결함 패턴 집중 훈련 가능 (guided 생성)
- **소속 기관**: IBM Thomas J. Watson Research Center (미국) + Siemens EDA (미국)

## OPC 툴 구현 관련성
- SKOPC 합성 레이아웃 생성 모듈 통합: 유도 무작위 레이아웃 생성
- `synthetic_layout_generator.py`: DRC 준수 무작위 레이아웃 자동 생성
- ML 결함 예측 모델을 SKOPC OPC 플로우 후처리로 통합
- 신규 노드 개발 초기 단계 OPC 레시피 검증 자동화 지원

## 태그
`SyntheticLayout`, `MachineLearning`, `DefectPrediction`, `HotspotDetection`, `OPC`, `M1Pinching`, `LineEnd`, `TechnologyNode`, `Calibre`, `IBM`, `Siemens`, `SPIE`, `2025`
