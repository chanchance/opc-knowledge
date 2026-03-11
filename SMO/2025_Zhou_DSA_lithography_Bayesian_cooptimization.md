# Fully Automated Inverse Co-Optimization of Templates and Block Copolymer Blending Recipes for DSA Lithography

## 메타데이터
- **저자**: Yuhao Zhou, Huangyan Shen, Qingliang Song, Qingshu Dong, Jianfeng Li, Weihua Li
- **연도**: 2025
- **게재지/학회**: arXiv:2510.02715 (physics.comp-ph / cs.AI / cs.CE)
- **DOI/URL**: https://arxiv.org/abs/2510.02715
- **인용수**: 신규 논문

## 핵심 요약
sub-7nm 기술 노드에서 접촉공(contact hole) 및 수직 연결(VIA) 제조를 위한 DSA(Directed Self-Assembly) 블록 공중합체 리소그래피의 완전 자동화 역 공동 최적화 방법을 제안한 논문. 2개 파라미터만으로 템플릿 형상을 기술하는 가우시안 기술자(Gaussian descriptor)와 베이지안 최적화(Bayesian Optimization)를 결합하여 다양한 다중 공 패턴에서 최적 템플릿과 블렌드 조합을 효율적으로 탐색한다.

## 주요 기여
- 2파라미터 가우시안 기술자로 DSA 템플릿 형상 저차원 파라미터화
- AB/AB 이진 블렌드(binary blend) 활용으로 다양한 템플릿 기하구조 적응성 향상
- 템플릿 형태와 블렌드 파라미터의 베이지안 공동 최적화
- 최적화 중 곡률 변동 제약으로 제조 실현 가능성(manufacturability) 보장
- 다중 공 패턴에서 넓은 조정 가능 윈도우(tunable window) 유지

## 알고리즘/수식
- **가우시안 기술자**:
  - 템플릿 형상 T(x,y) = A · exp(-(x²/σ_x² + y²/σ_y²))
  - 파라미터: (σ_x, σ_y) — 2차원 가우시안 폭
  - 복잡한 템플릿을 2개 파라미터로 근사

- **베이지안 최적화 프레임워크**:
  ```
  θ* = argmin_{θ=(σ_x, σ_y, x_blend)} f(θ)
  ```
  - f(θ): DSA 시뮬레이션 품질 지표 (공 형상 오차)
  - GP(Gaussian Process) 대리 모델로 f 근사
  - 획득 함수(acquisition function): EI(Expected Improvement) 또는 UCB

- **곡률 제약**:
  - κ(t) = |γ''(t)| / |γ'(t)|³ ≤ κ_max (최대 곡률 한계)
  - 베이지안 최적화 제약 조건으로 설정

- **AB/AB 이진 블렌드**:
  - 순수 AB 다이블록 대신 두 종류의 AB 다이블록 혼합
  - 블렌드 비율 x_blend ∈ [0,1]이 추가 최적화 변수

## OPC 툴 구현 관련성
SKOPC의 미래 확장으로 DSA 리소그래피 지원 시 핵심 참조 논문. DSA는 EUV 다음 세대의 패터닝 기술로, sub-7nm 이하에서 필수적. 베이지안 최적화 접근은 SKOPC의 `skopc/pwo/` PWO 모듈에서 공정 윈도우 파라미터 탐색에도 응용 가능. 가우시안 기술자의 저차원 파라미터화는 복잡한 소스 형상 표현에도 참고 가능.

## 참고문헌 (핵심)
- 베이지안 최적화 원전: Srinivas et al. (2010), Shahriari et al. (2016)
- DSA 리소그래피 관련: Bates et al., 블록 공중합체 자기조립
- DSA 다중 패터닝: arXiv:1902.04145

## 태그
`DSA`, `directed-self-assembly`, `block-copolymer`, `Bayesian-optimization`, `template-optimization`, `sub-7nm`, `co-optimization`, `Gaussian-descriptor`, `2025`, `arxiv`
