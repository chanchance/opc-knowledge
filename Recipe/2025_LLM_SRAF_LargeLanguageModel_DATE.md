# LLM-SRAF: Sub-Resolution Assist Feature Generation Using Large Language Model

## 메타데이터
- **저자**: (CUHK Bei Yu 그룹)
- **연도**: 2025
- **게재지**: Design, Automation & Test in Europe Conference (DATE 2025)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10993108
- **인용수**: ~5

## 핵심 요약
대규모 언어 모델(LLM)을 활용하여 SRAF를 자동 생성하는 LLM-SRAF 방법을 제안한다. Meta-Llama-3.1-8B 기반 파운데이션 모델을 미세 조정하여, SRAF 생성 태스크 설명, OPC 레시피, 리소그래피 조건, 마스크 규칙, 순차적 레이아웃 설명을 시맨틱 프롬프트 입력으로 받아 직접 SRAF를 생성한다. 기존 SOTA 방법 대비 PV Band 면적과 EPE 모두 개선하면서 모델 기반 방법보다 3배 이상 빠르다.

## 주요 기여
1. LLM(Llama-3.1-8B)을 SRAF 생성에 적응한 최초의 LLM 기반 SRAF 생성기
2. OPC 레시피, 리소그래피 조건, 마스크 규칙을 자연어 프롬프트로 통합
3. 순차적 레이아웃 설명으로 패턴 정보를 LLM에 전달
4. SOTA 대비 PVB/EPE 개선 + MB-SRAF 대비 3× 이상 빠름

## Recipe/Process Flow 상세

### LLM 기반 SRAF 생성의 동기
```
기존 SRAF 방법과 한계:
  Rule-based: 빠름, 단순 2D 한계
  Model-based SRAF: 정확, 매우 느림
  GAN 기반: 빠름, 복잡한 설계 조건 처리 어려움

LLM 적용 동기:
  LLM의 강점: 복잡한 규칙/조건 자연어로 이해
  OPC 레시피 = 복잡한 규칙 문서 → LLM 적합
  마스크 규칙(MRC): 문어체 규칙 → LLM 자연 처리
  설계 의도 이해: 레이아웃 컨텍스트 + 공정 요구사항

LLM-SRAF 아이디어:
  "이 레이아웃에 이 OPC 레시피/MRC 조건으로 SRAF를 배치하라"
  → LLM이 직접 SRAF 위치/크기 생성
```

### 시맨틱 프롬프트 설계
```
프롬프트 구조:
  1. 태스크 설명:
     "Generate SRAF for the following layout pattern..."
     목적, 역할, 제약 조건 명시

  2. OPC 레시피:
     리소그래피 파라미터: NA=0.33, λ=193nm
     레지스트 파라미터: σ, 임계값
     공정 변동 목표: DOF, EL 요구사항

  3. 마스크 규칙 (MRC):
     SRAF 최소 폭: w_min = X nm
     SRAF-주 패턴 최소 거리: d_min = Y nm
     SRAF 인쇄 방지 조건

  4. 순차적 레이아웃 설명:
     패턴 형상을 좌표 시퀀스로 직렬화:
       "Main feature: polygon at [(0,0),(200,0),(200,50)...]"
       "Neighbor: line at x=300, width=50nm, pitch=100nm"
     공간 관계: 패턴 간 거리, 밀도 정보

  5. 출력 형식 지정:
     "Output SRAF as: [(x1,y1,w1,h1), (x2,y2,w2,h2), ...]"
```

### LLM 미세 조정
```
파운데이션 모델: Meta-Llama-3.1-8B
  80억 파라미터 트랜스포머
  강력한 자연어 이해 + 생성 능력

훈련 데이터:
  (레이아웃 설명, OPC 레시피, MRC) → SRAF 배치 쌍
  Ground Truth: Model-based SRAF 결과

미세 조정 방법:
  LoRA (Low-Rank Adaptation): 효율적 파라미터 조정
  손실: 생성 SRAF 좌표 vs. Ground Truth SRAF 위치

특화 토큰:
  좌표, 파라미터 값을 특수 토큰으로 표현
  공간 관계 명시적 인코딩

추론:
  새 레이아웃 + 레시피 → 프롬프트 생성 → Llama 추론 → SRAF
```

### 성능 결과
```
기준: SOTA SRAF 방법 (GAN-SRAF, CTM-SRAF, RB-SRAF)

PV Band 면적:
  LLM-SRAF: SOTA 대비 감소

EPE:
  LLM-SRAF: SOTA 대비 개선

속도:
  LLM-SRAF: MB-SRAF 대비 3× 이상 빠름
  GAN-SRAF와 유사한 추론 속도

장점:
  유연성: OPC 레시피/MRC 프롬프트로 쉬운 조건 변경
  새 노드 적응: 프롬프트만 수정 → 새 공정 적용
  해석 가능: 자연어 프롬프트 → 결정 이유 이해 가능
```

## OPC 툴 구현 관련성
- **SKOPC LLM-SRAF**: `skopc/modeling/sraf_generator.py`에 LLM-SRAF 백엔드 추가
- **레시피 통합**: YAML OPC 레시피 → LLM 프롬프트 자동 변환 파이프라인
- **MRC 규칙 자연어화**: SKOPC MRC 규칙을 LLM 프롬프트로 변환
- **신규 노드**: 프롬프트 수정만으로 신규 공정 노드 LLM-SRAF 적응

## 참고문헌
- DATE 2025
- 저자 소속: CUHK (Bei Yu 그룹)
- 관련: CTM-SRAF (TCAD 2023)
- 관련: LLM-HD (DAC 2024)
- 관련: GAN SRAF placement (SPIE 11613, 2021)

## 태그
`Recipe`, `DATE`, `SRAF`, `LLM`, `LargeLanguageModel`, `Llama`, `GenerativeAI`, `PromptEngineering`, `ProcessWindow`, `CUHK`, `BeiYu`, `2025`
