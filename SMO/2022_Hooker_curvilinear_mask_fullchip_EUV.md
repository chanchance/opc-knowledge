# Curvilinear Mask Solutions for Full-Chip EUV Lithography

## 메타데이터
- **저자**: Kevin Hooker, Guangming Xiao, et al.
- **연도**: 2022
- **게재지**: Proc. SPIE 12054, Novel Patterning Technologies 2022, 1205407 (25 May 2022)
- **DOI/URL**: https://doi.org/10.1117/12.2618392

## 핵심 요약
다중 빔 마스크 라이터 기술을 활용하여 전체 칩 EUV 리소그래피에서 곡선형(curvilinear) 마스크 솔루션을 구현하는 방법을 제안한다. ILT, ML ILT + 곡선형 OPC, 맨해튼 OPC의 세 가지 접근법을 전체 칩 수준에서 리소그래피 성능 및 런타임 측면에서 비교 평가한다.

## 주요 기여
1. **전체 칩 곡선형 마스크 비교**: 맨해튼 OPC vs 곡선형 ILT vs ML ILT + 곡선형 OPC 정량 비교
2. **ML ILT 가속**: 머신러닝 기반 ILT로 전체 칩 적용 가능한 런타임 달성
3. **하이브리드 파이프라인**: ML ILT를 초기값으로 사용, 곡선형 OPC로 정밀 조정
4. **실용적 구현**: 실제 EUV 레이어에서 곡선형 마스크 풀-칩 적용 가능성 시연

## 알고리즘/수식
### 세 가지 마스크 합성 방법 비교
```
방법 1: 맨해튼 OPC (기준선)
  - 직각 세그먼트 기반 마스크 패턴
  - 빠른 런타임, 제한된 공정 창

방법 2: 곡선형 ILT (최고 품질)
  - 픽셀화 마스크 최적화: min_M ||I_sim(M) - I_target||² + λ·R(M)
  - 곡선형 마스크 자연 생성
  - 느린 런타임 (전체 칩 비실용적)

방법 3: ML ILT + 곡선형 OPC (하이브리드)
  - ML ILT: 신경망으로 빠른 초기 마스크 예측
  - 곡선형 OPC: 시뮬레이션 기반 세밀 조정
  - 균형: ILT에 근접한 품질 + OPC 수준 속도
```

### 평가 지표
- EPE(Edge Placement Error): 타겟 대비 인쇄 오차
- 공정 창(PW): DOF × EL 곱
- 런타임(TAT): 전체 칩 기준 시간

## OPC 툴 SMO 구현 관련성
- 곡선형 마스크 OPC의 실용적 풀-칩 구현 방법론
- ML ILT + OPC 하이브리드: SKOPC 마스크 합성 모듈의 딥러닝 가속 설계 참조
- SMO와 곡선형 마스크: 소스 최적화 결과를 ML ILT 입력으로 활용하는 파이프라인

## 태그
`ILT`, `OPC`, `EUV`, `curvilinear_mask`, `full_chip`, `ML_ILT`, `multi_beam_writer`, `SPIE`
