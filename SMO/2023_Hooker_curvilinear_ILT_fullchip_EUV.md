# Enhancing Mask Synthesis for Curvilinear Masks in Full-Chip Extreme Ultraviolet Lithography

## 메타데이터
- **저자**: Kevin Hooker, Guangming Xiao, Yu-Po Tang, Yunqiang Zhang, Moongyu Jeong, John Valadez, Kevin Lucas
- **연도**: 2023
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 22, Issue 4, 041606 (December 20, 2023)
- **DOI/URL**: https://doi.org/10.1117/1.JMM.22.4.041606

## 핵심 요약
다중 빔 마스크 라이터(multi-beam mask writer) 기술 발전으로 곡선형(curvilinear) 마스크가 고급 EUV 리소그래피 세대로 확장 가능해졌다. ILT는 곡선형 마스크 친화적 마스크 합성 방법이지만 기존 rule-based SRAF + OPC보다 TAT(Turn-Around Time)이 느리다. 이를 해결하기 위해 ILT와 곡선형 OPC를 결합한 하이브리드 솔루션을 제안한다.

## 주요 기여
1. **하이브리드 곡선형 마스크 솔루션**: ILT + 곡선형 OPC 결합으로 ILT 품질과 OPC 속도를 동시 달성
2. **ML 기반 ILT 가속**: 머신러닝 ILT + 곡선형 OPC 파이프라인으로 전체 칩 적용 가능한 TAT 달성
3. **Cubic Bezier 곡선 OPC**: 데이터 볼륨 제어를 위한 3차 베지에 곡선 기반 곡선형 OPC
4. **전체 칩 성능 비교**: 맨해튼 OPC vs 곡선형 ILT vs 하이브리드 ML ILT + 곡선형 OPC 정량 비교

## 알고리즘/수식
### 하이브리드 곡선형 마스크 합성 파이프라인
```
단계 1: ML ILT (빠른 초기 솔루션)
  - 학습된 신경망으로 마스크 패턴 예측
  - 입력: 타겟 레이아웃 패턴
  - 출력: 곡선형 마스크 초기값

단계 2: 곡선형 OPC (정밀 조정)
  - ML ILT 출력을 초기값으로 곡선형 OPC 수행
  - 시뮬레이션 기반 EPE 최소화
  - 곡선 파라미터 최적화

단계 3: Cubic Bezier 표현
  - 마스크 윤곽선을 3차 베지에 곡선으로 표현
  - 데이터 볼륨 제어: 제어점 수 최소화
```

### Cubic Bezier 곡선 표현
```
B(t) = (1-t)³P₀ + 3(1-t)²tP₁ + 3(1-t)t²P₂ + t³P₃, t∈[0,1]

여기서:
- P₀, P₃: 끝점 (곡선 경계)
- P₁, P₂: 제어점 (곡률 결정)
- 장점: 적은 수의 제어점으로 복잡한 곡선 표현 가능
```

### 성능 지표
- EPE(Edge Placement Error): 타겟 대비 인쇄 오차
- TAT(Turn-Around Time): 전체 칩 마스크 합성 소요 시간
- 데이터 볼륨: 마스크 파일 크기 (곡선형은 맨해튼 대비 증가)

## OPC 툴 SMO 구현 관련성
- 곡선형 마스크 지원 OPC의 최신 방법론: SKOPC 마스크 합성에서 비-맨해튼 패턴 지원 아키텍처 참조
- ML ILT + 곡선형 OPC 하이브리드: 딥러닝 기반 OPC 가속과 물리 기반 정밀 OPC의 결합
- Bezier 곡선 표현: EUV ILT 마스크의 데이터 볼륨 관리 방법
- SMO와의 통합: 곡선형 마스크를 고려한 소스 최적화 필요성 시사

## 태그
`ILT`, `OPC`, `EUV`, `curvilinear_mask`, `full_chip`, `ML_ILT`, `Bezier_curve`, `multi_beam_writer`, `JMNM`, `SPIE`
