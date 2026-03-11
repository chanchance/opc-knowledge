# SemiKong: Curating, Training, and Evaluating A Semiconductor Industry-Specific Large Language Model

## 메타데이터
- **저자**: Christopher Nguyen, William Nguyen, Atsushi Suzuki, Daisuke Oku, Hong An Phan, Sang Dinh, Zooey Nguyen, Anh Ha, Shruti Raghavan, Huy Vo, Thang Nguyen, Lan Nguyen, Yoshikuni Hirayama
- **연도**: 2024
- **게재지/학회**: arXiv:2411.13802
- **DOI/URL**: https://arxiv.org/abs/2411.13802
- **인용수**: N/A (2024년 출판)

## 핵심 요약
SemiKong은 반도체 도메인 최초의 산업 특화 대형 언어 모델(LLM)로, 도메인 특화 코퍼스 큐레이션과 전문화된 사전 학습으로 개발되었다. 525.6M 토큰의 반도체 전문 텍스트로 Llama3를 파인튜닝하여 반도체 제조 용어 및 공정 흐름에 대한 광범위한 지식을 갖춘 7B/70B 파라미터 모델을 제공한다. OPC 레시피 자동화를 포함한 반도체 제조 태스크에서 일반 목적 LLM을 능가한다.

## 주요 기여
- **SemiKong-Corpus**: 기술 도서, 연구 논문, 특허에서 수집한 반도체 특화 텍스트 (525.6M 토큰)
- **SemiKong-Trainer**: 7B 및 70B 파라미터 기반 모델 (Llama3 기반)
- **SemiKong-Eval**: 전문가 피드백을 통합한 도메인 특화 평가 프레임워크
- **반도체 제조 특화**: 에칭, 리소그래피, OPC 등 제조 공정에 특화

## Recipe/Process Flow 상세

### 2단계 훈련 방법론

**단계 1: 사전 훈련 (Pre-training)**
- Llama3 체크포인트에서 반도체 전문 텍스트로 파인튜닝
- 데이터셋 구성:
  - 129개 기술 도서/챕터
  - 708개 에칭 관련 논문
  - 20,000개 연구 논문
- 총 525.6M 토큰

**단계 2: 지도 파인튜닝 (Supervised Fine-tuning)**
- 50,000개 지침-응답 쌍으로 구성된 데이터셋
- 개념 이해, 복잡한 에칭 문제, 표준 공정 이슈 포함

### 전문가 평가 프레임워크 (SemiKong-Eval)
전문가 참여 검증을 통해 개발된 6가지 평가 기준:
1. **명확성 및 직접성 (C&D)**: 기술 내용의 명확한 전달
2. **실용성 및 즉시 활용성 (PIU)**: 현장 적용 가능성
3. **효율성 및 간결성 (E&B)**: 간결한 전문 표현
4. **논리적 흐름 및 일관성 (LFC)**: 공정 설명의 논리적 구조
5. **전문가 간 소통 (EEC)**: 전문가 수준의 기술 언어
6. **예시 및 구체성 활용 (UES)**: 구체적 예시와 수치

### OPC/리소그래피 관련 능력
- 에칭 공정 이해: 습식/건식/플라즈마/RIE 에칭 변형
- 리소그래피 공정 흐름 이해
- OPC 레시피 관련 용어 및 개념 이해
- 제조 공정 파라미터 해석 및 설명

### 성능 결과
- SemiKong-70B: 24.02 집계 점수
- Llama3-70B: 22.35 집계 점수
- 상용 모델 대비 도메인 관련 지표에서 우수

## OPC 툴 구현 관련성
- **OPC 레시피 자동화 인터페이스**: SemiKong을 OPC 레시피 설정 및 설명을 위한 자연어 인터페이스 백엔드로 활용
- **레시피 문서 생성**: OPC 레시피 파라미터 설명 및 문서 자동 생성
- **공정 문제 진단**: OPC 레시피 실행 중 발생하는 공정 문제 자연어 진단 지원
- **설계 규칙 해석**: DRC/MRC/LRC 규칙을 자연어로 설명하고 해석하는 인터페이스
- **Intelligent OPC 어시스턴트**: Chen et al. (2024)의 Intelligent OPC Engineer Assistant와 통합 가능한 LLM 백엔드

## 참고문헌 (핵심)
- ChipNemo (NVIDIA): 칩 설계 특화 LLM
- RTLCoder: RTL 코드 생성 LLM
- ChipGPT: 칩 설계 GPT
- Llama3 (Meta): 기반 모델

## 태그
`SemiKong`, `LLM`, `Semiconductor`, `Manufacturing`, `Etching`, `Lithography`, `OPC Recipe`, `Domain-specific AI`, `Recipe`, `OPC`, `Llama3`, `Fine-tuning`, `Natural Language Interface`
