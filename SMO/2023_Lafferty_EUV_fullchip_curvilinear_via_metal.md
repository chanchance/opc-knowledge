# EUV Full-Chip Curvilinear Mask Options for Logic Via and Metal Patterning

## 메타데이터
- **저자**: Neal Lafferty, et al.
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950K (28 April 2023)
- **DOI/URL**: https://doi.org/10.1117/12.2647882

## 핵심 요약
다중 빔 마스크 라이팅 기술로 곡선형 마스크를 통한 최대 리소그래피 공정 창 실현이 가능해졌다. ILT가 이상적인 곡선형 패턴을 생성하지만 전체 칩 로직 제조에는 런타임이 너무 느리다. 이 논문은 3nm 노드 비아 및 메탈 예시에서 대안적 접근법을 검토하고, 전체 ILT, 하이브리드 ILT, 조밀 곡선형 OPC, ML 접근법의 런타임과 리소그래피 메트릭을 비교한다.

## 주요 기여
1. **3nm 노드 비아/메탈 곡선형 마스크 비교**: 실제 3nm 노드 레이어에서 4가지 방법 비교
2. **ML 접근법 런타임 분석**: 전체 ILT 대비 ML 기반 접근법의 속도 이점 정량화
3. **조밀 곡선형 OPC**: 높은 밀도 패턴에서 곡선형 OPC의 적용 가능성
4. **실용적 트레이드오프 분석**: 리소그래피 성능 vs 런타임 트레이드오프 제공

## 알고리즘/수식
### 4가지 접근법 비교
```
1. 전체 ILT (Full ILT):
   - 최고 리소그래피 품질
   - 전체 칩에 비실용적 런타임

2. 하이브리드 ILT (Hybrid ILT):
   - ILT + OPC 조합
   - 품질과 속도의 균형

3. 조밀 곡선형 OPC (Dense Curvilinear OPC):
   - 조밀 패턴에 특화된 곡선형 OPC
   - 맨해튼 OPC 대비 향상된 공정 창

4. ML 접근법:
   - 신경망 기반 빠른 마스크 예측
   - 전체 칩 규모 적용 가능
```

### 타겟 노드
- 3nm 노드 로직
- 비아(Via) 레이어: 40nm 이하 피치
- 메탈(Metal) 레이어: 극저 k1 조건

## OPC 툴 SMO 구현 관련성
- 3nm 노드 EUV 곡선형 마스크 OPC의 최신 현황
- ML 기반 OPC 가속: SKOPC 딥러닝 모듈 방향 제시
- 비아/메탈 레이어에서 곡선형 마스크의 실용적 한계와 가능성
- SMO 출력(최적 소스 + 마스크)과 곡선형 OPC 통합 플로우

## 태그
`ILT`, `OPC`, `EUV`, `curvilinear_mask`, `full_chip`, `3nm_node`, `via_patterning`, `metal_patterning`, `ML_OPC`, `DTCO`, `SPIE`
