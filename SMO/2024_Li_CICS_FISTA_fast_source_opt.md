# Fast Lithographic Source Optimization Adopting a Certain Interval Contour Sampling Compressive Sensing

## 메타데이터
- **저자**: Zhen Li, Yanqiu Li, He Yang, Miao Yuan, Zhiwei Zhang, Weichen Huang, Zhaoxuan Li
- **연도**: 2024
- **게재지/학회**: Applied Optics, Vol. 63, No. 36, pp. 9103–9109
- **DOI/URL**: https://doi.org/10.1364/AO.536534
- **인용수**: 확인 필요

## 핵심 요약
일정 간격 등고선 샘플링(Certain Interval Contour Sampling, CICS)과 빠른 반복 수축 임계값 알고리즘(FISTA)을 결합한 압축 센싱 소스 최적화(CICS-FISTA-SO) 방법을 제안한다. Nesterov 가속 기술로 FISTA를 가속하여 빠른 소스 최적화와 고충실도 이미징을 동시에 달성한다. 기존 CCS-BCS-SO 대비 2.23배 빠른 속도와 3.5% 낮은 모드 오차를 달성한다.

## 주요 기여
- 일정 간격 등고선 샘플링(CICS)으로 샘플 포인트 균일 분포 보장
- Nesterov 가속 FISTA로 수렴 속도 대폭 향상
- CCS-BCS-SO 대비 2.23배 속도 향상, 3.5% 오차 감소
- 빠른 소스 최적화와 고충실도 이미징의 균형 달성

## 알고리즘/수식
**CICS-FISTA-SO 목적함수:**
$$\min_{\boldsymbol{a}} \|\boldsymbol{a}\|_1 \quad \text{s.t.} \quad \|T_{CICS}\Phi\boldsymbol{a} - \boldsymbol{b}_{CICS}\|_2^2 \leq \epsilon$$
일정 간격 등고선 샘플링 행렬 $T_{CICS}$ 기반 소스 계수 재구성.

**일정 간격 등고선 샘플링 (CICS):**
등고선 포인트를 일정 간격 $\Delta s$로 샘플링:
$$\{x_j\}_{j=1}^{N_{CICS}} \subset \text{contour}(mask), \quad \|x_{j+1} - x_j\| = \Delta s$$
균일 간격으로 등고선 샘플링 → 균형 잡힌 측정값 확보.

**FISTA (Fast ISTA with Nesterov Acceleration):**
$$y^{(t+1)} = \boldsymbol{a}^{(t)} + \frac{t-1}{t+2}(\boldsymbol{a}^{(t)} - \boldsymbol{a}^{(t-1)})$$
Nesterov 모멘텀 항으로 수렴 가속.

$$\boldsymbol{a}^{(t+1)} = \text{shrink}\left(y^{(t+1)} - \frac{1}{L}\nabla g(y^{(t+1)}), \frac{\lambda}{L}\right)$$
수축 연산자로 l1 최소화.

**수렴 속도 비교:**
- ISTA: $O(1/t)$ 수렴
- FISTA (Nesterov): $O(1/t^2)$ 수렴
→ 2.23× 속도 향상 달성.

**성능 결과 (vs. CCS-BCS-SO):**
- 속도: 2.23× 빠름
- 평균 모드 오차: 3.5% 감소

## OPC 툴 SMO 구현 관련성
- SKOPC 소스 최적화에서 CICS+FISTA 결합으로 빠른 CS 소스 최적화 구현
- `skopc/smo/cics_fista_source_opt.py`에 일정 간격 등고선 샘플링 FISTA 소스 최적화
- Sun et al. 2019 CCS-BCS-SO의 개선 버전으로 함께 참고
- Nesterov 가속 FISTA는 다른 CS 기반 소스/마스크 최적화에도 적용 가능

## 참고문헌 (핵심)
- Sun et al., "CCS-BCS fast SO," Optics Express 2019
- Sun et al., "Fast nonlinear CS SMO Newton-IHTs," Optics Express 2019
- Song et al., "Inverse litho source opt CS," Optics Express 2014

## 태그
`SMO`, `Applied-Optics`, `compressive-sensing`, `CICS`, `FISTA`, `Nesterov-acceleration`, `contour-sampling`, `source-optimization`, `fast-SO`, `l1-minimization`, `convergence`
