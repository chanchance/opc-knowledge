# Physics-Informed Neural Networks and Neural Operators for EUV Electromagnetic Wave Diffraction from a Lithography Mask

## 메타데이터
- **저자**: Vasiliy A. Es'kin, Egor V. Ivanov
- **연도**: 2025
- **게재지/학회**: arXiv:2507.04153 (math.NA / cs.AI / cs.LG / physics.comp-ph / physics.optics)
- **DOI/URL**: https://arxiv.org/abs/2507.04153
- **인용수**: 신규 논문

## 핵심 요약
EUV 리소그래피 마스크의 전자기파 회절 문제를 풀기 위한 물리 정보 신경망(PINN) 및 신경 연산자(Neural Operator)를 개발한 논문. 핵심 혁신은 WGNO(Waveguide Neural Operator)로, 파도파관(waveguide) 방법의 가장 계산 비용이 큰 부분을 신경망으로 대체하는 하이브리드 접근법이다. 현실적인 2D 및 3D 마스크 기하구조에서 최고 수준의 정확도와 추론 속도를 달성한다.

## 주요 기여
- EUV 마스크 회절을 위한 PINN 및 신경 연산자 개발
- WGNO(Waveguide Neural Operator): 파도파관 방법 + 신경망 하이브리드
- 기존 방법 대비 정확도와 계산 속도 모두 향상
- 현실적인 2D 및 3D EUV 마스크 기하구조에서 검증
- 복잡한 전자기 회절 문제의 신경망 가속화 새 기준 제시

## 알고리즘/수식
- **EUV 마스크 회절 물리**:
  - Maxwell 방정식: ∇×E = -∂B/∂t, ∇×H = J + ∂D/∂t
  - 3D 마스크 구조에서 완전 벡터 회절 계산 필요
  - 근접장(near-field) → 원거리장(far-field) 전파

- **파도파관 방법**:
  - 마스크를 수직 방향 슬라이스로 분할
  - 각 슬라이스에서 고유 모드 계산 → 전파 행렬 곱
  - 계산 비용: O(N_modes² × N_slices)

- **WGNO (Waveguide Neural Operator)**:
  - 파도파관의 고유 모드 계산 부분을 NO로 대체
  - NO: mask_geometry → eigenmode_coefficients
  - 하이브리드: NO_고유 + 수치적_전파행렬
  - 추론 시 O(1) 복잡도 (훈련 후)

- **PINN 접근**:
  - Maxwell PDE를 신경망 손실에 포함:
    L_PDE = ||∇×E_NN + ∂B_NN/∂t||² + ||∇×H_NN - J - ∂D_NN/∂t||²
  - 경계 조건 손실 L_BC 추가

## OPC 툴 구현 관련성
SKOPC의 EUV 마스크 모델링 정확도 향상에 장기 활용 가능. 현재 `LithoEngine`이 스칼라 회절 근사를 사용하는 반면, WGNO는 완전 벡터 EUV 마스크 효과(3D 마스크 효과, 그림자 효과)를 정확하게 모델링 가능. EUV 7nm 이하 노드에서 3D 마스크 효과가 중요해지므로, `skopc/modeling/litho_engine.py`의 EUV 모드 확장에 WGNO 통합 고려.

## 참고문헌 (핵심)
- Maxwell 방정식 수치해법 (RCWA, FEM, FDTD)
- Pomplun et al., FEM 기반 EUV 마스크 시뮬레이션 (JCO 시리즈)
- Physics-Informed Neural Networks 원전: Raissi et al. (2019)
- Fourier Neural Operator: Li et al. (2021)

## 태그
`EUV`, `PINN`, `neural-operator`, `waveguide`, `Maxwell-equations`, `3D-mask-effect`, `electromagnetic-diffraction`, `lithography-simulation`, `2025`, `arxiv`
