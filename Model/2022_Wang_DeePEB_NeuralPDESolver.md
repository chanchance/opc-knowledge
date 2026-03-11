# DeePEB: A Neural Partial Differential Equation Solver for Post Exposure Baking Simulation in Lithography

## 메타데이터
- **저자**: Qipan Wang, Xiaohan Gao, Yibo Lin, Runsheng Wang, Ru Huang
- **연도**: 2022
- **게재지/학회**: IEEE/ACM International Conference on Computer-Aided Design (ICCAD 2022)
- **DOI/URL**: https://doi.org/10.1145/3508352.3549398; GitHub: https://github.com/Brilight/DeePEB
- **인용수**: 40+

## 핵심 요약
PEB(Post Exposure Bake, 노광 후 베이킹) 시뮬레이션을 위한 신경망 기반 편미분방정식(PDE) 솔버 DeePEB를 제안한 논문. PEB 공정은 리소그래피에서 aerial image와 최종 레지스트 프로파일 사이를 연결하는 핵심 단계이나, PDE 수치 해법의 높은 계산 비용으로 인해 compact 모델이나 생략으로 처리되어 왔다. DeePEB는 PEB 과정을 지배하는 연립 PDE를 신경망으로 근사하여, 상업용 엄밀 시뮬레이션 대비 100배 이상의 가속과 높은 정확도를 동시에 달성한다.

## 주요 기여
- PEB 시뮬레이션에 특화된 신경망 PDE 솔버 최초 제안
- 상업용 엄밀 PEB 시뮬레이터 대비 100배 이상 가속
- PEB 과정의 coupled PDE를 신경망으로 정확히 근사
- 리소그래피 모델링 ML 분야에서 PEB 시뮬레이션 공백 해결
- 효율적이고 정확한 레지스트 프로파일 예측 가능

## 모델 아키텍처/수식
**PEB 물리 모델 (coupled PDEs):**

산 농도 A(x, y, z, t) 확산:
```
∂A/∂t = D_A(T) · ∇²A - k_q · A · B
```

염기(quencher) 농도 B(x, y, z, t):
```
∂B/∂t = D_B(T) · ∇²B - k_q · A · B
```

여기서:
- D_A(T), D_B(T): 온도 의존 확산 계수 (Arrhenius 관계)
- k_q: 산-염기 중화 반응 상수
- T: PEB 온도 (공간적으로 균일 가정)
- 경계조건: 기판/공기 계면에서 무플럭스(no-flux) 조건

**DeePEB 신경망 구조:**
Physics-informed 신경망 접근:

```
Input: 초기 산 농도 분포 A₀(x, y, z) + PEB 조건 (T, t_bake)
       ↓
[Encoder: 3D Conv layers] → 잠재 표현(latent)
       ↓
[Temporal Evolution Module: Neural ODE / Transformer]
  dh/dt = f_θ(h, t)   (신경망으로 PDE 우변 근사)
       ↓
[Decoder: 3D TransposeConv] → A(x, y, z, t_final), B(x, y, z, t_final)
```

**손실 함수 (Physics-informed):**
```
L = L_data + λ_pde · L_PDE + λ_bc · L_BC

L_data = ||A_pred - A_GT||² + ||B_pred - B_GT||²

L_PDE = ||∂A_pred/∂t - D_A·∇²A_pred + k_q·A_pred·B_pred||²
       + ||∂B_pred/∂t - D_B·∇²B_pred + k_q·A_pred·B_pred||²

L_BC = ||∇A_pred · n̂||²_boundary  (경계 조건)
```

**PEB 후 레지스트 현상 연결:**
```
A_peb(x, y) = ∫ A(x, y, z, t_bake) dz    (z-방향 적분)
CD = f(A_peb; T_dev, σ_dev)               (현상 모델)
```

**성능:**
- 속도: 상업용 시뮬레이터 대비 >100×
- 정확도: CD 예측 오차 < 0.5nm
- 3D 레지스트 프로파일 예측 지원

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 `LithoEngine(process.optical, process.resist)` 내 PEB 시뮬레이션 가속화 방안으로 활용 가능. TorchResist가 해석적 PEB 모델을 사용하는 반면, DeePEB는 더 정밀한 PDE 기반 PEB 시뮬레이션을 신경망으로 가속한다. `skopc/modeling/` 내 고정밀 레지스트 모델이 필요한 경우(EUV 7nm 이하 노드)에 DeePEB 통합 고려. GitHub 코드 공개로 직접 통합 가능.

## 참고문헌 (핵심)
- Mack, C.A., "Lumped parameter model for chemically amplified resists," SPIE 5377 (2004)
- Raissi, M. et al., "Physics-informed neural networks," Journal of Computational Physics (2019)
- Chen, R.T.Q. et al., "Neural ordinary differential equations," NeurIPS 2018
- Willson, C.G. et al., "Post-exposure bake modeling," Willson Research Group (2002)

## 태그
`Model`, `OPC`, `ResistModel`, `PEB`, `PostExposureBake`, `PDE`, `NeuralODE`, `PhysicsInformed`, `Diffusion`, `CAR`, `3D`, `ICCAD`, `DeepLearning`
