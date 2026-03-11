# Open-Source Differentiable Lithography Imaging Framework

## 메타데이터
- **저자**: Guojin Chen, Hao Geng, Bei Yu, David Z. Pan
- **연도**: 2024
- **게재지/학회**: arXiv:2409.15306; SPIE Advanced Lithography + Patterning 2024 (Vol. 12954)
- **DOI/URL**: https://arxiv.org/abs/2409.15306; https://doi.org/10.1117/12.3009980
- **인용수**: 30+

## 핵심 요약
미분 가능한(differentiable) 오픈소스 리소그래피 이미징 프레임워크 TorchLitho를 소개하는 논문. GPU 병렬 연산과 자동 미분(autograd)을 활용하여 표준 스칼라 이미징 모델(Abbe 및 Hopkins 모델)을 완전히 미분 가능한 형태로 구현한다. 오픈소스 최초로 Abbe 리소그래피 모델, 해석적 레지스트 현상 모델, 벡터 리소그래피 구현을 포함하며, 새로운 리소그래피 기반 ML 알고리즘 개발을 위한 표준 플랫폼을 제공한다.

## 주요 기여
- 오픈소스 최초 미분 가능한 Abbe 리소그래피 이미징 모델 구현
- Hopkins/TCC 모델의 미분 가능 버전 제공
- 오픈소스 최초 해석적 레지스트 현상(development) 모델 포함
- GPU 가속 기반 end-to-end 미분 가능 파이프라인 구축
- PyTorch 기반으로 ML 알고리즘과 완벽히 통합 가능
- 벡터(vector) 리소그래피 구현 (작업 중)

## 모델 아키텍처/수식
**Abbe 모델 (부분 간섭, Partially Coherent Imaging):**
```
I(x) = Σₖ |hₖ ⊗ m(x)|²
```
여기서:
- hₖ: k번째 광원점에 대응하는 coherent 점 확산 함수(PSF)
- m(x): 마스크 투과율 함수
- ⊗: 합성곱 연산

**Hopkins 모델 (TCC 기반):**
```
I(x) = ΣΣ TCC(f, f') · M(f) · M*(f') · exp(j2π(f-f')x) df df'
```
TCC (Transmission Cross Coefficient):
```
TCC(f, f') = ∫ S(f₀) · H(f+f₀) · H*(f'+f₀) df₀
```
- S(f₀): 광원 강도 분포
- H(f): 투영 렌즈 전달 함수(pupil function)

**SVD 기반 TCC 커널 분해:**
```
TCC ≈ Σₙ λₙ · φₙ · φₙ†   (n개의 커널로 근사)
I(x) ≈ Σₙ λₙ · |φₙ ⊗ m(x)|²
```

**레지스트 현상 모델 (해석적):**
```
R(x) = sigmoid((I(x) - T) / σ_r)
```
- T: 현상 임계값
- σ_r: sigmoid 기울기 (레지스트 대비)

**미분 가능성 활용 (gradient 기반 최적화):**
```
∂L/∂m = ∂L/∂I · ∂I/∂m   (chain rule via autograd)
```
마스크 최적화: m ← m - α · ∂L/∂m

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 핵심 의존성인 TorchLitho의 공식 논문. `skopc/modeling/` 내 `LithoEngine` 구현이 이 프레임워크를 기반으로 한다. 미분 가능한 시뮬레이터를 통해 gradient 기반 ILT/OPC 최적화가 가능하며, GNN-OPC 학습 시 손실 함수 역전파에 직접 활용. GitHub: https://github.com/TorchOPC/TorchLitho. SKOPC에서 TorchLitho import 시 이 논문의 Abbe/Hopkins 구현을 참조하면 모델 파라미터 의미 이해에 도움.

## 참고문헌 (핵심)
- Hopkins, H.H., "On the diffraction theory of optical images," Proc. R. Soc. London A, 217, 1953
- Abbe, E., "Beiträge zur Theorie des Mikroskops," Archiv für Mikroskopische Anatomie, 9, 1873
- Mack, C.A., "Fundamental principles of optical lithography," Wiley, 2007
- Yang, H. et al., "GAN-OPC," DAC 2018 / TCAD 2020
- Chen, G. et al., "DAMO: Deep agile mask optimization," ICCAD 2021

## 태그
`Model`, `OPC`, `OpticalModel`, `Hopkins`, `Abbe`, `TCC`, `TorchLitho`, `OpenSource`, `Differentiable`, `GPU`, `PyTorch`, `ResistModel`, `ILT`
