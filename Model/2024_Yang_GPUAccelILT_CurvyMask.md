# GPU-Accelerated Inverse Lithography Towards High Quality Curvy Mask Generation

## 메타데이터
- **저자**: Haoyu Yang, Haoxing Ren (NVIDIA)
- **연도**: 2024 (arXiv), 2025 (ISPD 발표)
- **게재지/학회**: arXiv:2411.07311; ACM International Symposium on Physical Design (ISPD 2025)
- **DOI/URL**: https://arxiv.org/abs/2411.07311; https://doi.org/10.1145/3698364.3705343
- **인용수**: 신규 (2024년 11월 발표)

## 핵심 요약
GPU 가속과 곡선형(curvilinear) 마스크 생성에 특화된 ILT 알고리즘을 제안한 논문. 다중 빔 마스크 묘화기(MBMW: Multi-Beam Mask Writer) 기술 발전으로 가능해진 자유형 곡선 마스크가 인쇄 웨이퍼 이미지 품질과 공정 윈도우를 크게 향상시키지만, 기존 ILT는 맨해튼(Manhattan) 기하학에 최적화되어 있다는 한계가 있다. 이 논문은 더 나은 곡률과 마스크 아티팩트 감소를 위해 특별히 설계된 알고리즘으로 직접 곡선형 ILT를 생성하며, 오픈 벤치마크에서 선도적인 학술 ILT 엔진 대비 큰 우위를 입증한다.

## 주요 기여
- 곡선형 마스크 직접 생성을 위한 GPU 가속 ILT 알고리즘
- 더 나은 곡률과 마스크 아티팩트 감소를 위한 특화 설계
- 컨투어 품질, 공정 윈도우 동시 개선
- 오픈 벤치마크에서 최신 학술 ILT 대비 유의미한 성능 우위
- NVIDIA cuLitho 플랫폼의 곡선형 마스크 지원 기반 기술

## 모델 아키텍처/수식
**곡선형 마스크의 필요성:**

Manhattan 마스크 (기존):
```
M(x, y) ∈ {0, 1}  (이진 격자)
엣지: 수평/수직선만 허용
```

Curvilinear 마스크 (MBMW 지원):
```
M(x, y) ∈ [0, 1]  (연속 또는 임의 형상)
엣지: 자유형 곡선 허용
```

**GPU 가속 ILT (Gradient 기반):**
```
목적함수:
E(M) = L_print(M, Z) + λ_PVB·PVBand(M, Z) + μ·L_mask_rule(M)

Gradient 계산:
∂E/∂M = ∂L_print/∂M + λ_PVB·∂PVBand/∂M + μ·∂L_mask_rule/∂M
```
GPU 병렬화: 각 마스크 픽셀 독립 업데이트 → 대규모 병렬 연산

**곡률 개선을 위한 특화 알고리즘:**

곡률 정규화 항:
```
L_curvature = ∫ κ²(s) ds   (마스크 엣지 곡률 제곱 적분)
κ(s): 엣지 곡률 (2차 미분 관련)
```

마스크 아티팩트 제거:
```
L_artifact = ||∇²M||²   (급격한 변화 페널티)
```

**전체 손실:**
```
E(M) = ||Litho(M) - Z||²
     + λ_PVB · PVBand(M, Z)
     + μ_curv · L_curvature
     + μ_art · L_artifact
     + ν · L_mask_rule(M)
```

**GPU 최적화:**
- H100 GPU에서 배치 처리: 수백 타일 동시 최적화
- Gradient 계산: TorchLitho autograd 활용
- 수렴 가속: Adam optimizer + 적응형 학습률

**마스크 규칙 검사 (MRC):**
```
L_mask_rule = Σᵢ max(0, min_feature_size - size_i)²
            + Σᵢ max(0, min_gap - gap_i)²
```
(파운드리/EDA 공급업체에서 개발 중)

**성능 (오픈 벤치마크):**
- 컨투어 품질: 기존 Manhattan ILT 대비 유의미한 향상
- 공정 윈도우: PVBand -15~20% 개선
- 속도: CPU ILT 대비 40× (cuLitho 기반)

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 장기 로드맵에서 곡선형 마스크 지원을 위한 핵심 참조. 현재 SKOPC의 GNN-OPC가 세그먼트 변위(Manhattan geometry)를 예측하는 것에서, 곡선형 마스크 지원으로 확장 시 이 논문의 곡률 정규화 방법론 적용. `skopc/pwo/` NSGA-II 최적화에서 곡선형 마스크 생성 시 L_curvature와 L_artifact를 추가 목적함수로 통합 가능. cuLitho 통합 시 이 논문의 GPU 가속 ILT 알고리즘 기반.

## 참고문헌 (핵심)
- NVIDIA cuLitho: https://developer.nvidia.com/culitho
- Yang, H. et al., "ILILT," ICML 2024
- Yang, H. et al., "CFNO+LGST," arXiv:2207.04056 (2022)
- Yang, H. and Ren, H., "Enabling scalable AI computational lithography," ASPDAC 2023

## 태그
`Model`, `OPC`, `ILT`, `CurvilinearMask`, `GPU`, `cuLitho`, `MBMW`, `MaskQuality`, `ProcessWindow`, `NVIDIA`, `ISPD`, `GradientDescent`, `CurvatureRegularization`
