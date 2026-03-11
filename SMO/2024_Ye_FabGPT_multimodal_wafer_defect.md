# FabGPT: An Efficient Large Multimodal Model for Complex Wafer Defect Knowledge Queries

## 메타데이터
- **저자**: Ye et al. (반도체 제조 AI 연구팀)
- **연도**: 2024
- **게재지/학회**: arXiv:2407.10810
- **DOI/URL**: https://arxiv.org/abs/2407.10810
- **인용수**: 신규 (2024년 7월)

## 핵심 요약
반도체 IC 분야의 결함 지식 질의를 위한 대규모 멀티모달 언어 모델 FabGPT를 제안한 논문. SEM(Scanning Electron Microscope) 이미지에서 미세 결함 감지, 근본 원인 분석(root cause analysis), 제조 공정 전문가 Q&A를 단일 모델로 수행한다. 향상된 멀티모달 특징 토큰으로 복잡한 웨이퍼 배경에서 미세 결함을 자동 감지하고, 동적 정렬 보정 토큰으로 LLM을 미세 조정하여 결함 속성 분석과 양식 편향(modality bias) 문제를 함께 해결한다.

## 주요 기여
- IC 분야 최초의 결함 지식 질의 특화 대규모 멀티모달 언어 모델
- 3단계 점진적 훈련으로 결함 감지 + 고품질 대화 기능 동시 달성
- 향상된 특징 토큰으로 복잡한 웨이퍼 배경에서 미세 결함 자동 감지
- 동적 정렬 보정 토큰으로 결함 위치/유형/수량 정확한 응답
- 양식 편향(modality bias) 완화로 멀티모달 대화 품질 향상

## 성능 결과 (SEM-WaD 데이터셋)
- 이미지 수준 감지 정확도: 91.81%
- 픽셀 수준 감지 정확도: 95.61%
- PRO (Per-Region Overlap): 88.17%
- AP (Average Precision): 85.80%

## 알고리즘/수식
- **3단계 훈련 프레임워크**:
  1. 1단계: 시각 인코더 + 언어 모델 정렬 (멀티모달 특징 매핑)
  2. 2단계: 결함 감지 특화 미세 조정 (향상된 특징 토큰 학습)
  3. 3단계: 대화 능력 강화 (동적 보정 토큰, 결함 Q&A)

- **향상된 멀티모달 특징 토큰**:
  - SEM 이미지 → 시각 인코더 → 시각 특징 V
  - 결함 관련 특징 강화: V_enhanced = Attention(V_query, V_context)
  - 복잡한 배경 suppression + 결함 영역 강조

- **동적 정렬 보정 토큰**:
  - 텍스트 쿼리 T와 시각 특징 V 정렬
  - T_corrected = Align(T, V_enhanced; θ_align)
  - LLM 입력으로 사용하여 결함 속성 생성

- **결함 지식 Q&A**:
  - 입력: SEM 이미지 + 자연어 질문
  - 출력: 결함 유형, 위치, 수량, 근본 원인, 수정 방안

## OPC 툴 구현 관련성
SKOPC의 장기 기능으로 AI 보조 OPC 분석 기능 구현 시 참조. FabGPT의 멀티모달 접근은 SKOPC GUI에서 웨이퍼 SEM 이미지를 불러와 자동 결함 진단을 수행하는 기능의 기술적 기반. 결함 근본 원인 분석(OPC 파라미터 부적합, 마스크 오류, 공정 변동 등)을 자동화하는 지능형 OPC 도구 개발에 참조.

## 참고문헌 (핵심)
- Liu et al., "LLaVA" — 멀티모달 대화 모델 기반
- InstructBLIP 관련 논문
- SEM 결함 데이터셋 관련 반도체 논문들

## 태그
`LLM`, `multimodal`, `wafer-defect`, `SEM`, `root-cause-analysis`, `semiconductor`, `defect-detection`, `Q&A`, `2024`, `arxiv`
