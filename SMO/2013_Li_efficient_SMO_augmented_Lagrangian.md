# Efficient Source and Mask Optimization with Augmented Lagrangian Methods in Optical Lithography

## 메타데이터
- **저자**: Jia Li, Shiyuan Liu, Edmund Y. Lam
- **연도**: 2013
- **게재지/학회**: Optics Express, Vol. 21, No. 7, pp. 8076–8090
- **DOI/URL**: https://doi.org/10.1364/OE.21.008076
- **인용수**: 다수

## 핵심 요약
22nm 이하 공정 기술에서 소스-마스크 최적화의 복잡도 제어와 수렴 효율 향상을 위해 증강 라그랑지안(Augmented Lagrangian) 방법을 적용한 SMO 알고리즘을 제안한다. 복잡도 패널티를 등식 제약으로 정식화하여 증강 라그랑지안 함수를 구성하고, 준-뉴턴(quasi-Newton) 방법으로 두 부분 문제를 교대로 최소화하여 수렴 속도를 향상시키고 전체 실행 시간을 단축한다.

## 주요 기여
- 복잡도 패널티를 등식 제약으로 포함하는 증강 라그랑지안 SMO 정식화
- 준-뉴턴 방법 기반 교대 최소화로 수렴 가속
- 패널티 파라미터 자동 업데이트 전략
- 22nm 이하 공정에서 복잡도-성능 트레이드오프 효율적 제어

## 알고리즘/수식
**증강 라그랑지안 SMO 정식화:**
원래 문제를 등식 제약 문제로 변환:
$$\min_{\boldsymbol{\sigma}, m, \boldsymbol{z}} F(\boldsymbol{\sigma}, m) + R(z)$$
$$\text{s.t.} \quad \boldsymbol{x} = \boldsymbol{z}$$
여기서 $\boldsymbol{x} = [\boldsymbol{\sigma}; m]$, $R(\boldsymbol{z})$는 복잡도 패널티.

**증강 라그랑지안 함수:**
$$\mathcal{L}_\rho(\boldsymbol{x}, \boldsymbol{z}, \boldsymbol{y}) = F(\boldsymbol{x}) + R(\boldsymbol{z}) + \boldsymbol{y}^T(\boldsymbol{x} - \boldsymbol{z}) + \frac{\rho}{2}\|\boldsymbol{x} - \boldsymbol{z}\|^2$$
라그랑주 승수 $\boldsymbol{y}$와 패널티 파라미터 $\rho$.

**교대 최소화 (ADMM 유사):**
$$\boldsymbol{x}^{(t+1)} = \arg\min_{\boldsymbol{x}} \mathcal{L}_\rho(\boldsymbol{x}, \boldsymbol{z}^{(t)}, \boldsymbol{y}^{(t)})$$
$$\boldsymbol{z}^{(t+1)} = \arg\min_{\boldsymbol{z}} \mathcal{L}_\rho(\boldsymbol{x}^{(t+1)}, \boldsymbol{z}, \boldsymbol{y}^{(t)})$$
$$\boldsymbol{y}^{(t+1)} = \boldsymbol{y}^{(t)} + \rho(\boldsymbol{x}^{(t+1)} - \boldsymbol{z}^{(t+1)})$$

**준-뉴턴 방법 (L-BFGS) 기반 x-부분 문제 풀이:**
$$\boldsymbol{x}^{(t+1)} \approx \boldsymbol{x}^{(t)} - \alpha H_k^{-1} \nabla_{\boldsymbol{x}} \mathcal{L}_\rho$$
제한 메모리 BFGS로 Hessian 근사.

**패널티 파라미터 업데이트:**
$$\rho^{(t+1)} = \begin{cases} \tau \rho^{(t)} & \text{if } \|\boldsymbol{x}^{(t+1)} - \boldsymbol{z}^{(t+1)}\| > \epsilon_{dual} \\ \rho^{(t)} & \text{otherwise} \end{cases}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO의 증강 라그랑지안 기반 복잡도 제어 구현 시 핵심 참고
- `skopc/smo/admm_smo.py`에 ADMM 기반 SMO 구현 참고
- 소스/마스크 복잡도 패널티를 등식 제약으로 포함하는 정식화는 제조 가능성 제어에 유리
- Wu et al. 2014 Zernike SMO와 결합 시 Zernike 계수 복잡도 제어 가능

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Wu et al., "Zernike source representation SMO," Optics Express 2014
- Li & Lam, "SMPO Zernike pupil," SPIE 9052, 2014

## 태그
`SMO`, `Optics-Express`, `augmented-Lagrangian`, `ADMM`, `quasi-Newton`, `L-BFGS`, `complexity-penalty`, `constrained-optimization`, `alternating-minimization`, `convergence`, `22nm`
