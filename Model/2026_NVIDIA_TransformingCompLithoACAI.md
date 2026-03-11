# Transforming Computational Lithography with AC and AI -- Faster, More Accurate, and Energy-efficient

## 메타데이터
- **저자**: NVIDIA Research Team (Haoyu Yang, Haoxing Ren, 외)
- **연도**: 2026
- **게재지/학회**: arXiv:2602.15036 (February 2026)
- **DOI/URL**: https://arxiv.org/abs/2602.15036
- **인용수**: 신규 (2026년 2월 발표)

## 핵심 요약
가속 컴퓨팅(AC: Accelerated Computing)과 AI를 결합하여 계산 리소그래피를 혁신적으로 변환한 NVIDIA의 종합 성과 논문. cuLitho가 핵심 프리미티브(회절 광학, 계산 기하학, 다변수 최적화, 데이터 처리)를 재설계하여 end-to-end 57배 가속을 달성한다. AI는 계산 집약적 단계의 고충실도 서로게이트(surrogate)로 작동하여 AC에 추가적으로 평균 1.7배 속도 향상을 제공한다. OPC에서 12배 랙 감소, 13배 에너지 절감, 57배 계산 시간 단축을 입증한다.

## 주요 기여
- cuLitho 핵심 프리미티브 재설계: 57× end-to-end 가속
- AC + AI 결합: AC 위에 AI가 추가로 1.7× 속도 향상
- OPC에서: 12× 랙 감소 + 13× 에너지 절감 + 57× 계산 시간 단축
- 57× 속도 향상 → 13× 계산 탄소 배출 감소
- TSMC 생산 배포 실증

## 모델 아키텍처/수식
**cuLitho 핵심 프리미티브 재설계:**

**1. 회절 광학 (Diffractive Optics):**
기존 CPU TCC 계산:
```
TCC(f₁, f₂) = ∫ S(f) · H(f+f₁) · H*(f+f₂) df
  → 4D 행렬 계산 (O(N⁴))
```

cuLitho GPU 가속:
```
GPU 병렬화: 각 (f₁, f₂) 독립 계산
H100 GPU: 10,000+ 병렬 코어
속도 향상: CPU 대비 40~85×
```

**2. 계산 기하학 (Computational Geometry):**
마스크 패턴 처리의 GPU 가속:
```
Polygon clipping, Boolean ops → 병렬화
GPU 구현: CUDA 기반 병렬 기하 연산
```

**3. 다변수 최적화 (Multi-variant Optimization):**
OPC/ILT gradient 계산:
```
∂L/∂M = GPU_autograd(L, M)  (병렬 역전파)
mask_update = Adam(∂L/∂M)   (GPU 병렬 업데이트)
```

**4. AI 서로게이트 (AI Surrogate):**
계산 집약적 단계를 AI로 대체:
```
Litho_sim(M) → AI_surrogate_θ(M)
```
- 속도: 전통 시뮬레이터 대비 100×+
- 정확도: 1~5% 오차 허용

**AC + AI 결합 성능:**
```
기존 CPU OPC:  기준 시간 = 1×, 에너지 = 1×
cuLitho (AC):  시간 = 1/40×, 에너지 = ~1/13×
cuLitho + AI:  시간 = 1/57×, 에너지 = ~1/13×
```

**OPC 워크플로우 변환:**
```
기존: CPU cluster (40,000 CPUs, 2주)
cuLitho: GPU cluster (500 H100 GPUs, 1일)
cuLitho+AI: GPU cluster (500 H100 GPUs, 수 시간)
```

**환경 영향:**
```
탄소 배출 감소: 57× 속도 → 13× 배출 감소
이유: GPU 에너지 효율이 CPU보다 높기 때문
탄소 감소 < 속도 향상: GPU 전력 효율 차이
```

**산업 배포 (TSMC):**
- OPC 생산 워크플로우에 cuLitho 통합
- Synopsys Proteus OPC 엔진과 연동
- ASML 스캐너 파라미터 지원

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 장기 인프라 방향에서 가장 중요한 참조. 현재 SKOPC가 CPU 기반 TorchLitho를 사용하지만, cuLitho 방식의 GPU 가속 도입 시 이 논문의 프리미티브 재설계 방법 참조. 특히 `skopc/pwo/` NSGA-II PWO에서 수천 번의 시뮬레이션이 필요할 때 GPU 병렬화로 수십 배 속도 향상 가능. AI 서로게이트 통합으로 추가 1.7× 향상도 달성 가능. 탄소 효율성 측면도 OPC 툴의 지속 가능성 보고에 활용 가능.

## 참고문헌 (핵심)
- NVIDIA cuLitho: https://developer.nvidia.com/culitho
- Yang, H. et al., "Enabling scalable AI computational lithography," ASPDAC 2023
- Yang, H. et al., "GPU-accelerated ILT curvy mask," ISPD 2025
- Yang, H. et al., "CFNO + LGST," arXiv:2207.04056 (2022)
- TSMC + NVIDIA collaboration: https://blogs.nvidia.com/blog/tsmc-culitho-computational-lithography/

## 태그
`Model`, `OPC`, `cuLitho`, `GPU`, `NVIDIA`, `AcceleratedComputing`, `AI`, `Energy`, `TSMC`, `Synopsys`, `Production`, `57x`, `Speedup`, `CarbonReduction`, `2026`
