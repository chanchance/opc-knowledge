# Large Scale Mask Optimization Via Convolutional Fourier Neural Operator and Litho-Guided Self Training (CFNO)

## 메타데이터
- **저자**: Haoyu Yang, Zongyi Li, Kumara Sastry, Saumyadip Mukhopadhyay, Anima Anandkumar, Brucek Khailany, Vivek Singh, Haoxing Ren
- **연도**: 2022
- **게재지/학회**: arXiv preprint (준비 중), arXiv:2207.04056
- **DOI/URL**: https://arxiv.org/abs/2207.04056
- **기관**: NVIDIA, Caltech

## 핵심 요약
CFNO는 Convolutional Fourier Neural Operator와 리소그래피 유도 자기학습(LGST)을 결합하여 대규모 풀칩 마스크 최적화를 가능하게 하는 프레임워크다. 기존 ML 기반 OPC가 소규모 단일 클립에 집중하던 한계를 넘어, 타일 간 스티칭 아티팩트 없이 대규모 레이아웃을 처리한다. 최초로 ML 기반 프레임워크가 최고 수준 학술 수치 마스크 최적화기를 능가하며, 동시에 수 배 이상의 속도 향상을 달성한다.

## 주요 기여
- **CFNO 아키텍처**: 레이아웃 타일 간 의존성을 효율적으로 학습하는 Convolutional Fourier Neural Operator
- **스티칭 아티팩트 제거**: 대규모 레이아웃 처리 시 타일 경계 아티팩트 없는 연속적 마스크 최적화
- **리소그래피 유도 자기학습(LGST)**: 비볼록 최적화 문제에서 모델과 데이터셋을 반복적으로 개선하는 자기학습 전략
- **SOTA 초과 달성**: 최초로 ML 기반 방법이 학술 수치 마스크 최적화기 성능 초과 + 수십 배 속도 향상

## Recipe/Process Flow 상세

### CFNO 대규모 마스크 최적화 파이프라인

```
풀칩 레이아웃 입력
        ↓
[타일 분할 (Tile Partitioning)]
  - 오버랩 윈도우로 타일 분할
  - 타일 의존성 그래프 구성 (인접 타일 관계 파악)
        ↓
[CFNO 모델 추론]
  입력: 타일 레이아웃 이미지
  처리:
    1. 로컬 특성 추출 (Conv 레이어)
    2. 전역 타일 의존성 학습 (FNO 유닛)
       - Fourier 변환 → 주파수 도메인 연산 → 역변환
       - Token-shared FNO: 대형 입력의 Fourier 변환 회피
    3. 마스크 생성 (디코더)
  출력: 최적화된 마스크 타일
        ↓
[리소그래피 유도 자기학습 (LGST)]
  반복 학습 루프:
    Step 1: 현재 모델로 마스크 생성
    Step 2: 리소그래피 시뮬레이션으로 품질 평가 (EPE, PVB)
    Step 3: 고품질 마스크를 새 학습 데이터로 추가
    Step 4: 확장된 데이터로 모델 재학습
    Step 5: 수렴까지 반복
        ↓
[타일 재조합]
  - 오버랩 영역 블렌딩으로 스티칭 아티팩트 제거
  - 전체 칩 마스크 재구성
        ↓
풀칩 최적화 마스크 출력
```

### CFNO 아키텍처 상세

**Fourier Neural Operator (FNO) 핵심 원리**:
$$\mathcal{F}[v_{l+1}](k) = R_{\phi}(k) \cdot \mathcal{F}[v_l](k)$$
- $\mathcal{F}$: 이산 푸리에 변환
- $R_{\phi}$: 학습 가능한 주파수 도메인 필터
- 전역적 컨텍스트를 효율적으로 캡처 (O(N log N) 복잡도)

**Token-shared FNO 유닛**:
- 표준 FNO의 대형 입력 처리 문제 해결
- 타일 단위 Fourier 변환으로 계산 효율성 유지
- 타일 간 의존성을 크로스-어텐션으로 캡처

**CFNO = Conv 로컬 특성 + FNO 전역 의존성**:
```
타일 이미지 → Conv 레이어 (로컬 패턴)
             + FNO 유닛 (전역 타일 관계) → 마스크 생성
```

### LGST 자기학습 전략 상세
비볼록 최적화 문제에서의 반복적 개선:
1. **초기 학습**: 기존 ILT/OPC 데이터로 CFNO 초기 학습
2. **생성 단계**: 학습된 CFNO로 대규모 레이아웃의 마스크 생성
3. **평가 단계**: 리소그래피 시뮬레이터로 생성 마스크 품질 점수화
4. **선택 단계**: 품질 임계값 이상의 마스크를 새 학습 쌍으로 선택
5. **재학습 단계**: 확장된 데이터셋으로 CFNO 재학습
6. **반복**: 성능 수렴까지 2-5 반복

### 성능 지표
- 학술 최고 수준 ILT 엔진 대비 EPE, PVB 모두 향상
- 처리 속도: 기존 수치 최적화기 대비 10배 이상 가속
- 스티칭 없는 대규모 처리: 이전 ML 방법 대비 핵심 차별점

## OPC 툴 구현 관련성
CFNO의 접근법은 SKOPC 풀칩 처리 기능 강화에 활용 가능:
- **풀칩 OPC 처리**: SKOPC recipe_runner.py의 배치 처리에 CFNO 기반 타일 처리 통합
- **FNO 기반 리소그래피 시뮬레이터**: litho_engine.py를 FNO로 대체하여 전역 컨텍스트 반영
- **LGST 자기학습**: SKOPC GNN-OPC 모델 성능 개선을 위한 자기학습 파이프라인 구축
- **스티칭 처리**: 대형 GDS 파일 처리 시 타일 경계 문제 해결 전략

## 참고문헌 (핵심)
- Li et al., "Fourier Neural Operator for Parametric Partial Differential Equations" (ICLR 2021)
- Yang et al., "GAN-OPC" (IEEE TCAD 2020)
- Chen et al., "DAMO" (ICCAD 2020)
- Anandkumar et al., "Neural Operator: Graph Kernel Network for Partial Differential Equations" (2019)

## 태그
`CFNO`, `Fourier Neural Operator`, `Large Scale`, `Mask Optimization`, `OPC`, `Self-Training`, `LGST`, `NVIDIA`, `Full Chip`, `Tile Optimization`, `2022`, `arXiv`
