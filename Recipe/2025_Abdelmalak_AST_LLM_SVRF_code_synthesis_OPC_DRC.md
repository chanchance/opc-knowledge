# An AST-guided LLM Approach for SVRF Code Synthesis

## 메타데이터
- **저자**: Abanoub E. Abdelmalak, Mohamed A. Elsayed, David Abercrombie, Ilhami Torunoglu
- **연도**: 2025
- **게재지/학회**: arXiv:2507.00352
- **DOI/URL**: https://arxiv.org/abs/2507.00352
- **인용수**: N/A (2025년 출판)

## 핵심 요약
SVRF(Standard Verification Rule Format) 코드 합성을 위한 AST(추상 구문 트리) 임베딩과 RAG(검색 증강 생성)를 통합한 새로운 방법론이다. 일반 사전 학습 LLM의 SVRF 적용 시 높은 환각률 문제를 해결하며, 740개 DRC 규칙 구현 벤치마크에서 기본 텍스트 파인튜닝 대비 40% 정확도 향상을 달성한다. OPC 규칙 자동 생성 및 DRC 규칙 코드 생성에 직접 적용 가능하다.

## 주요 기여
- **AST 임베딩 접근법**: ANTLR 문법으로 SVRF 코드를 계층적 AST로 파싱, LLM 토크나이저용 선형화
- **AST 가중 손실 함수**: 명령어, 옵션, 레이어 순서의 중요도에 따라 차등 패널티
- **RAG 통합**: 구문 특성과 물리 검증 의도로 인덱싱된 SVRF 코드 스니펫 검색
- **40% 향상**: 기본 텍스트 파인튜닝 대비 코드 생성 정확도 40% 향상

## Recipe/Process Flow 상세

### SVRF 코드 합성 파이프라인

**단계 1: AST 구성 (ANTLR 기반)**
1. ANTLR 문법으로 SVRF 코드 파싱 → 파스 트리 생성
2. 중복 제거 및 노드 유형 표준화 → 추상 AST 생성
3. 깊이 우선 순회로 AST를 괄호 문자열로 직렬화
4. LLM 토크나이저 입력 형식으로 변환

**단계 2: AST 가중 손실 함수 학습**
- 명령어 정확도 (c_acc): 높은 가중치 (핵심 SVRF 명령어)
- 옵션 정확도 (o_acc): 중간 가중치
- 레이어 순서 정확도 (l_acc): 높은 가중치 (순서 중요)
- 후보-정답 AST 구조 비교로 차등 패널티 적용

**단계 3: RAG 통합**
- 컨텍스트 검색: 구문 특성 + 물리 검증 의도로 인덱싱된 SVRF 스니펫 매칭
- 지식 그래프 통합: 내부 데이터셋을 AST 표현에 매핑
- 프롬프트 향상: 검색된 패턴으로 풍부한 컨텍스트 제공

**단계 4: T5 기반 모델 생성**
- CodeT5-base (220M), Flan-T5-base (250M), T5-base (220M) 중 선택
- AST 가이드 파인튜닝으로 SVRF 문법 및 의미론 학습
- 표준 사전 학습 어휘로도 SVRF 문법 적응 가능

### SVRF 코드 복잡도 분류
| 규칙 유형 | 예시 수 | 비율 |
|-----------|---------|------|
| 단순 규칙 | 241개 | 32.5% |
| 중간 규칙 | 347개 | 46.8% |
| 복잡 규칙 | 153개 | 20.7% |

### 맞춤형 SVRF 평가 지표 (AST-Weighted Accuracy)
- 명령어 정확도 (c_acc)
- 옵션 정확도 (o_acc)
- 레이어 순서 정확도 (l_acc)

전통적 지표: BLEU, ROUGE-L

### 실험 결과 (CodeT5 with AST)
- 검증: 63.796% AST 가중 정확도, BLEU 0.876, ROUGE-L 0.916
- 테스트: 62.879%, BLEU 0.840, ROUGE-L 0.898
- 검증-테스트 갭: 0.917%p (강건한 일반화)
- 기본 파인튜닝 대비: 40% 정확도 향상

### 계산 비용
- AST 표현으로 토큰 수 ~3배 증가 (10토큰 → 30+ 토큰)
- 훈련 시간: 33% 증가 (6시간 → 8시간, NVIDIA H100 NVL)
- 메모리: 40% 증가
- 결과: 성능 향상 + 데이터 증강 필요성 감소로 상쇄

## OPC 툴 구현 관련성
- **OPC 규칙 자동 생성**: SVRF는 OPC 규칙 포맷으로, AST-LLM으로 OPC runset 자동 생성 가능
- **DRC-OPC 통합 레시피**: 자연어 설명에서 DRC/OPC SVRF 규칙 코드 자동 생성
- **OPC 레시피 문서화**: 기존 SVRF OPC 규칙을 자연어로 설명하는 역방향 변환
- **설계 규칙 위반 수정**: LLM이 DRC 위반을 분석하고 SVRF 수정 코드 자동 생성
- **SRAF 규칙 코드 생성**: SRAF 삽입 규칙을 SVRF 코드로 자동 변환하는 OPC 레시피 도구

## 참고문헌 (핵심)
- T5 (Raffel et al., 2020): 기반 언어 모델
- CodeT5 (Wang et al., 2021): 코드 특화 T5
- ANTLR4: 파서 생성기
- RAG (Lewis et al., 2020): 검색 증강 생성

## 태그
`SVRF`, `LLM`, `AST`, `RAG`, `DRC`, `OPC Rule`, `Code Synthesis`, `CodeT5`, `T5`, `Recipe`, `OPC`, `EDA Automation`, `Design Rule`, `Runset Generation`
