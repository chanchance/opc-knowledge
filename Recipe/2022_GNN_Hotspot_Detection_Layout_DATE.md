# Efficient Hotspot Detection via Graph Neural Network

## 메타데이터
- **저자**: (CUHK Bei Yu 그룹, DATE 2022)
- **연도**: 2022
- **게재지**: 2022 Design, Automation & Test in Europe Conference (DATE 2022)
- **DOI/URL**: https://www.cse.cuhk.edu.hk/~byu/papers/C134-DATE2022-GNN-HSD.pdf
- **인용수**: ~45

## 핵심 요약
레이아웃 핫스팟 검출을 위한 그래프 신경망(GNN) 기반 효율적 방법을 제안한다. 레이아웃을 그래프로 변환하는 새로운 표현 모델을 도입하여 레이아웃 구성 요소와 그 지역 기하학적 관계를 인코딩하고, 수정된 GNN으로 핫스팟을 분류한다. ICCAD 2012 컨테스트 벤치마크에서 10배 이상의 속도 향상과 정확도 손실 없이 낮은 오경보율을 달성한다.

## 주요 기여
1. 레이아웃을 그래프로 매핑하는 새로운 표현 모델 (다차원 특징)
2. 지역 기하학적 관계 임베딩을 위한 수정 GNN 구조
3. ICCAD 2012 벤치마크에서 10× 이상 속도 향상
4. CNN 기반 방법 대비 낮은 오경보율 달성

## Recipe/Process Flow 상세

### 핫스팟 검출의 중요성
```
리소그래피 핫스팟:
  정의: OPC 후에도 인쇄 결함 발생 가능성이 높은 레이아웃 패턴
  유형:
    - 브리지 (Bridging): 인접 피처 단락
    - 브레이크 (Breaking): 피처 단절
    - 소면적 (Small area): 너무 작은 패턴 영역
  발생: 복잡한 2D 패턴, 공정 변동 하에서

핫스팟 검출 목적:
  조기 발견: 설계 단계에서 레이아웃 수정 → 제조 비용 절감
  OPC 선행: OPC 전에 문제 패턴 식별 → OPC 최적화 우선순위
  수율 예측: 핫스팟 밀도 → 칩 수율 상관관계
```

### 레이아웃 그래프 표현
```
레이아웃 → 그래프 변환:
  노드 (Node): 레이아웃 도형 단위
    - 직선 엣지 세그먼트
    - 코너 점
    - 다각형 패치
  특징 (Node Feature):
    - 기하학: 길이, 폭, 방향각
    - 컨텍스트: 이웃 패턴 정보
    - 공간: 절대/상대 좌표

  엣지 (Edge): 도형 간 관계
    - 공간 근접성: 거리 < 임계값 → 엣지 생성
    - 위상 연결성: 같은 다각형 → 내부 엣지
  특징 (Edge Feature):
    - 거리: 노드 간 간격
    - 방향: 상대 방향 벡터
    - 유형: 근접/연결 구분

장점:
  불규칙 레이아웃 자연스럽게 처리
  국소 기하학 명시적 인코딩
  회전/이동 불변 특징 가능
```

### GNN 아키텍처
```
수정된 GNN 구조:
  메시지 전달 (Message Passing):
    h_v^(k) = UPDATE(h_v^(k-1), AGGREGATE({h_u^(k-1) : u ∈ N(v)}))
    N(v): v 노드의 이웃 집합

  특화 설계:
    - 엣지 특징 통합: 거리/방향 가중치 집계
    - 다층 집계: k=3~5 레이어 (국소→광역 컨텍스트)
    - 어텐션: 중요 이웃 노드에 집중

  분류기:
    그래프 풀링: 노드 임베딩 → 그래프 수준 표현
    MLP: 핫스팟 확률 출력 (이진 분류)
    임계값: 핫스팟/비핫스팟 결정

훈련:
  레이블: 리소그래피 시뮬 기반 핫스팟 위치
  손실: 이진 교차 엔트로피 + 클래스 불균형 처리
  데이터 증강: 회전, 플립으로 훈련 다양성 확보
```

### 성능 결과
```
ICCAD 2012 컨테스트 벤치마크:
  검출 정확도:
    핫스팟 검출률: CNN 기반 방법과 동등
    오경보율: CNN 대비 감소 (정밀도 향상)
    F1 스코어: 경쟁력 있는 성능

  속도:
    CNN 기반 방법: 슬라이딩 윈도우 방식 → 느림
    GNN 방법: 그래프 직접 처리 → 10× 이상 빠름
    → 전체 칩 규모 실용적 핫스팟 검출 가능

비교:
  패턴 매칭 (Rule-based): 빠르지만 새 패턴 대응 불가
  CNN 슬라이딩 윈도우: 정확하지만 느림
  GNN: 빠름 + 정확 + 낮은 오경보율
```

## OPC 툴 구현 관련성
- **SKOPC 핫스팟 검출**: GNN 기반 OPC 전/후 핫스팟 사전 검출로 OPC 우선순위 결정
- **레이아웃 그래프**: SKOPC 레이아웃 DB → 그래프 표현 변환 모듈 추가
- **OPC 예측**: 핫스팟 GNN → OPC 수렴 어려운 패턴 조기 식별
- **전체 칩**: 10× 속도 향상으로 전체 칩 핫스팟 스캔 실용화

## 참고문헌
- DATE 2022; PDF: https://www.cse.cuhk.edu.hk/~byu/papers/C134-DATE2022-GNN-HSD.pdf
- 저자 소속: CUHK (Bei Yu 그룹)
- 관련: LLM-HD hotspot detection (DAC 2024)
- 관련: ICCAD 2012 Hotspot Detection Contest
- 관련: GNN-OPC (ResGNN edge displacement, SKOPC Phase 7)
- 관련: BridgingHotspot-MaskOpt domain crossing (TODAES 2025)

## 태그
`Recipe`, `DATE`, `HotspotDetection`, `GNN`, `GraphNeuralNetwork`, `Layout`, `Lithography`, `MachineLearning`, `CUHK`, `BeiYu`, `ICCAD2012`, `2022`
