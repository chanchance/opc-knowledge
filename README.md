# OPC Knowledge Base

A comprehensive collection of **718+ academic papers** on Optical Proximity Correction (OPC) for semiconductor lithography, organized into 4 categories to support OPC tool development.

## Categories

| Category | Papers | Description |
|----------|--------|-------------|
| [SMO](./SMO/) | 228 | Source Mask Optimization |
| [Recipe](./Recipe/) | 234 | OPC Recipe & Process Flow |
| [Model](./Model/) | 132 | Optical / Resist / ML Models |
| [Verification](./Verification/) | 124 | LRC / EPE / Hotspot Verification |

Coverage: **1953–2026** · Sources: SPIE, IEEE, arXiv, ACM

---

## SMO — Source Mask Optimization

Papers on illumination source optimization, joint source-mask co-optimization, and SMO algorithms for advanced lithography nodes.

**Key topics:**
- Gradient-based SMO (Rosenbluth, Peng, Yu, Li)
- Pixelated / freeform illuminator optimization
- EUV SMO (thick mask, stochastic effects)
- High-NA anamorphic SMO
- ML/DL-based SMO (neural networks, diffusion models)
- Process window aware SMO

**Sample papers:**
- `2002_Rosenbluth_optimum_mask_source_patterns.md` — Foundational SMO theory
- `2005_Socha_simultaneous_SMO.md` — Simultaneous source-mask optimization
- `2011_Peng_gradient_SMO_optical_lithography.md` — Gradient-based SMO algorithm
- `2021_Tsai_fullchip_SMO_ASML_Brion.md` — Industrial full-chip SMO
- `2024_Chen_BiSMO_bilevel_source_mask.md` — Bilevel differentiable SMO

---

## Recipe — OPC Recipe & Process Flow

Papers on rule-based OPC, model-based OPC algorithms, SRAF insertion, ILT (Inverse Lithography Technology), and full OPC correction flows.

**Key topics:**
- Rule-based OPC (fragmentation, edge segment displacement)
- Model-based OPC convergence and correction flow
- SRAF / assist feature insertion algorithms
- Inverse Lithography Technology (ILT)
- Curvilinear mask optimization
- EUV OPC correction pipeline
- ML/DL-based mask optimization (GAN, CNN, RL, LLM)
- Double/multi-patterning OPC

**Sample papers:**
- `2004_Painter_Classical_Control_OPC_Convergence.md` — OPC convergence theory
- `2006_Barnes_ModelBased_SRAF_Placement_Optimization.md` — Model-based SRAF
- `2009_Li_DoublePatterning_Friendly_OPC.md` — LELE-aware OPC
- `2024_Chen_TorchLitho_OpenSource_DiffLitho.md` — Differentiable lithography framework
- `2024_Yang_CurvyILT_GPU_accelerated_inverse_lithography.md` — GPU-accelerated curvilinear ILT

---

## Model — Optical / Resist / ML Models

Papers on lithography simulation models: optical models (Hopkins/Abbe), resist models, etch models, mask 3D (M3D) models, and machine learning-based compact models.

**Key topics:**
- Hopkins diffraction / TCC kernel decomposition
- Compact resist models (VTR, LPM, CM0/CM1)
- EUV resist models (stochastic, dry resist)
- Etch proximity correction models
- Mask 3D electromagnetic models
- ML/DL lithography simulators (CNN, GAN, PINN, Transformer)
- Model calibration (CD-SEM, AIMS)

**Sample papers:**
- `1953_Hopkins_DiffractionTheoryOpticalImages.md` — Hopkins diffraction model (foundational)
- `1985_Mack_PROLITH_ComprehensiveOpticalLitho.md` — PROLITH simulator
- `1999_Cobb_VariableThresholdResistModel.md` — Variable threshold resist model
- `2023_Chen_Nitho_PhysicsInformedOpticalKernel.md` — Physics-informed optical kernel
- `2025_Wang_TorchResist_DifferentiableResist.md` — Differentiable resist simulator

---

## Verification — LRC / EPE / Hotspot Verification

Papers on OPC verification methodologies: lithography rule checks (LRC), edge placement error (EPE) analysis, mask verification, hotspot detection, and sign-off flows.

**Key topics:**
- Lithography Rule Check (LRC) and process window qualification
- Edge Placement Error (EPE) analysis and budget
- Mask Error Enhancement Factor (MEEF) verification
- Full-chip post-OPC simulation and sign-off
- Hotspot detection (rule-based, ML/DL)
- EUV stochastic defect verification
- Curvilinear mask verification (MRC, MDP)
- Process window band (PVB) prediction

**Sample papers:**
- `2005_Kim_MEEF_full_chip_model_based_verification.md` — Full-chip MEEF analysis
- `2007_Lee_LRC_process_window_error_detection.md` — 9-point PW LRC methodology
- `2021_Shiely_EPE_5nm_node_analysis.md` — 5nm EPE budget decomposition
- `2024_Wang_stochastic_OPC_cost_function_EUV.md` — Stochastic cost function for EUV OPC
- `2025_ML_guided_curvilinear_OPC_fast_accurate_manufacturable.md` — ML curvilinear OPC verification

---

## Paper Format

Each `.md` file follows a consistent structure:

```markdown
# {Paper Title}

## 메타데이터
- **저자**: {Authors}
- **연도**: {Year}
- **게재지/학회**: {Journal/Conference}
- **DOI/URL**: {Link}
- **인용수**: {Citations}

## 핵심 요약
{200-400 char summary}

## 주요 기여
- {Contribution 1}
- {Contribution 2}

## 알고리즘/수식 (or 검증 방법론)
{Key equations or methodology}

## OPC 툴 구현 관련성
{How this paper applies to OPC tool implementation}

## 참고문헌 (핵심)
{Key references}

## 태그
`{Category}`, `SPIE`/`IEEE`, `{additional tags}`
```

---

## Usage

This knowledge base is intended to support OPC tool development across four functional components:

```
Rule OPC → Model OPC → Calibration → Evaluation
              ↕
          SMO / ILT
              ↕
         Verification
```

- **SMO folder** → Source optimization engine implementation
- **Recipe folder** → OPC correction algorithm and flow
- **Model folder** → Lithography simulation model selection and calibration
- **Verification folder** → Post-OPC verification and sign-off engine

---

## Stats

- Total papers: **718**
- Year range: 1953–2026
- Primary sources: SPIE Advanced Lithography, IEEE TCAD, IEEE DAC, IEEE ICCAD, arXiv
- Languages: English (papers) + Korean (summaries)
