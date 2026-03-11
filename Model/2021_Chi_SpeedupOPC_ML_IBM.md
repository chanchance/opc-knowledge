# Speeding Up OPC by Leveraging Existing Designs with Machine Learning

## 메타데이터
- **저자**: Cheng Chi, Julian Dolby, Jeffrey C. Shearer, Derren Dunn, Sean Burns (IBM Thomas J. Watson Research Center)
- **연도**: 2021
- **게재지**: Proc. SPIE 11614, Design-Process-Technology Co-optimization XV, 116140N
- **DOI/URL**: https://doi.org/10.1117/12.2584621

## 핵심 요약
기존 설계(existing designs)의 리소그래피 타겟-OPC 마스크 쌍 데이터를 학습하여 새로운 설계에 ML 기반 OPC를 빠르게 적용하는 방법을 제안한다. PyTorch 및 다층 퍼셉트론을 IBM 클라우드에서 활용하여 전통적 OPC 대비 컴퓨팅 자원을 대폭 절감한다.

## 주요 기여
1. 기존 설계의 (target, OPC-mask) 쌍 데이터로 ML OPC 모델 학습
2. 학습된 ML 모델로 새 설계에 빠른 OPC 적용 (전통적 시뮬레이션 대체)
3. PyTorch 기반 MLP 아키텍처와 IBM 클라우드 분산 학습 활용
4. 전통적 OPC 대비 계산 자원 및 런타임 대폭 감소
5. 기존 OPC 데이터 재활용을 통한 데이터 효율적 학습 전략

## 모델 수식/아키텍처
- **ML OPC 모델**: layout_target(x,y) → opc_mask(x,y)
- **MLP 구조**:
  - 입력: 타겟 레이아웃 패치 (픽셀 기반 또는 엣지 기반 표현)
  - 은닉층: 다층 완전 연결층 (ReLU 활성화)
  - 출력: OPC 마스크 패치 (보정된 마스크 패턴)
- 학습 손실: L2 (마스크 픽셀 차이) 또는 리소그래피 시뮬레이션 기반 EPE 손실
- 전이 학습: 기존 설계 사전학습 → 새 설계 미세조정

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [x] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC에서 기존 OPC 결과 데이터베이스를 활용한 ML OPC 가속 모듈 구현 참조
- 반복 설계(memory, standard cell)에서 OPC 런타임 단축에 특히 효과적
- `2021_Chi_OPCSpeedup` 계열 논문으로 IBM의 ML OPC 접근 대표 사례
- `2020_ML_OPC_Sub5nm_Techniques.md`와 함께 ML OPC 런타임 개선 연구 계열

## 태그
`Model`, `OPC`, `ML`, `MLP`, `SpeedUp`, `TransferLearning`, `IBM`, `PyTorch`, `SPIE`, `DTCO`
