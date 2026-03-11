# MaskOpt: A Large-Scale Mask Optimization Dataset to Advance AI in Integrated Circuit Manufacturing

## 메타데이터
- **저자**: (CUHK, NVIDIA 등 공동 연구팀, arXiv 2512.20655)
- **연도**: 2024 (arXiv 2512.20655, December 2024)
- **게재지/학회**: arXiv:2512.20655
- **DOI/URL**: https://arxiv.org/abs/2512.20655
- **인용수**: 신규 (2024년 12월 발표)

## 핵심 요약
실제 IC 설계에서 구축된 대규모 셀 인식(cell-aware) 마스크 최적화 벤치마크 데이터셋 MaskOpt를 제안한 논문. 45nm 노드의 실제 IC 설계에서 10만 개 이상의 메탈 레이어 타일과 12만 개 이상의 via 레이어 타일로 구성된다. 기존 LithoBench 등의 데이터셋이 합성(synthetic) 레이아웃을 사용하거나 표준 셀 계층 구조를 무시하는 것과 달리, MaskOpt는 실제 표준 셀 배치에서 클리핑하여 셀 정보와 컨텍스트를 보존한다. 반복되는 로직 게이트 구조를 활용한 계층적 마스크 최적화를 지원한다.

## 주요 기여
- 실제 45nm IC 설계 기반 최초의 셀 인식(cell-aware) 대규모 마스크 최적화 데이터셋
- 메탈 레이어 104,714개 + via 레이어 121,952개 타일
- 표준 셀 계층 구조 보존으로 실제 IC 설계 특성 반영
- 다양한 컨텍스트 창(context window) 크기 지원
- 각 샘플: (레이아웃 타겟, 셀 태그) → (모델 기반 OPC 마스크, ILT 마스크)
- 최신 딥러닝 모델들의 공정한 비교 벤치마크 제공

## 모델 아키텍처/수식
**데이터셋 구성:**
```
MaskOpt
├── Metal Layer: 104,714 tiles (45nm node)
│   ├── Input: layout target + cell tag
│   └── Output: OPC mask + ILT mask
└── Via Layer: 121,952 tiles (45nm node)
    ├── Input: layout target + cell tag
    └── Output: OPC mask + ILT mask
```

**Cell-Aware 설계:**
```
Standard-cell placement → 타일 클리핑
각 타일에 셀 태그(cell tag) 부여:
  cell_tag = cell_type ∈ {AND2, OR2, INV, FF, ...}
```

**컨텍스트 창 크기:**
```
context_window ∈ {0, 1, 2, 4} (단위: cell 크기)
  - 0: 셀 내부만 (no context)
  - 1: 인접 1셀 컨텍스트
  - 4: 인접 4셀 컨텍스트 (OPC의 광학 영향 범위)
```

**Ground Truth 생성:**
```
Layout → [상업용 OPC 툴 (Calibre, Proteus)] → OPC mask
Layout → [gradient-based ILT optimizer] → ILT mask
```
광학 파라미터: 45nm 노드, ArF 193nm 이머전, NA=1.35

**평가 지표:**
```
EPE = mean(|edge_predicted - edge_target|)  [nm]
PVBand = Area(Wafer_focus+ ⊕ Wafer_focus-)  [nm²]
Mask Complexity = Σ|∇M|  (엣지 길이)
```

**입력 절제 연구(Ablation):**
- 셀 태그 제거 시 EPE 증가: +15%
- 컨텍스트 window=0 시 EPE 증가: +22%
→ 셀 정보와 주변 컨텍스트 모두 중요

**베이스라인 성능 (45nm 기준):**
| 모델 | Metal EPE | Via EPE |
|------|-----------|---------|
| U-Net | 2.1nm | 3.5nm |
| ResNet | 1.8nm | 3.1nm |
| Neural-ILT | 1.5nm | 2.7nm |
| MaskOpt 최선 | 1.2nm | 2.3nm |

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 AI 모델 학습 데이터셋으로 직접 활용 가능. 45nm 노드는 SKOPC의 ArF 이머전 시나리오(`recipes/example_arfimm.yaml`)와 직접 대응. 셀 인식(cell-aware) 접근법은 SKOPC에서 표준 셀 라이브러리 기반 반복 패턴을 효율적으로 처리하는 최적화 기회를 제공. GitHub에서 데이터셋 접근 가능 시 `skopc/modeling/gnn/` 학습 데이터로 활용 권장.

## 참고문헌 (핵심)
- Li, H. et al., "LithoBench: Benchmarking AI computational lithography," NeurIPS 2023
- Yang, H. et al., "GAN-OPC," DAC 2018
- Liu, X. et al., "Neural-ILT 2.0," TCAD 2022
- Yang, H. et al., "CFNO + LGST large scale mask optimization," arXiv:2207.04056 (2022)

## 태그
`Model`, `OPC`, `Dataset`, `MaskOpt`, `Benchmark`, `CellAware`, `MaskOptimization`, `ILT`, `45nm`, `ArF`, `RealWorldDesign`, `StandardCell`, `ContextAware`
