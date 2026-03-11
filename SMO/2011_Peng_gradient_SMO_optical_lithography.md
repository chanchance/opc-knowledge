# Gradient-Based Source and Mask Optimization in Optical Lithography

## 메타데이터
- **저자**: Yao Peng, Jinyu Zhang, Yan Wang, Zhiping Yu
- **연도**: 2011
- **게재지/학회**: IEEE Transactions on Image Processing, Vol. 20, No. 10, pp. 2856–2864
- **DOI/URL**: https://doi.org/10.1109/TIP.2011.2131668
- **인용수**: 다수 (SMO 분야 기초 논문)

## 핵심 요약
193nm 광학 리소그래피 수명 연장을 위한 픽셀 기반 Source and Mask Optimization (SMO) 프레임워크를 제안한다. 소스 최적화와 마스크 최적화를 통합하여 교번 반복 방식으로 공동 최적화하며, 목적함수의 그래디언트를 활용한 효율적인 수렴을 달성한다. SOCS(Sum of Coherent Systems) 분해를 기반으로 이미징 모델을 구성하여 계산 효율을 높인다.

## 주요 기여
- 픽셀 기반 소스 및 마스크의 그래디언트 기반 동시 최적화 프레임워크 제안
- 소스 최적화: 목적함수의 소스 픽셀 강도에 대한 해석적 그래디언트 도출
- 마스크 최적화: 이전 ILT 방법 개선, threshold-based sigmoid 투과율 모델 사용
- 193nm 공정에서 기존 방법 대비 공정 마진(process window) 유의미한 향상 실증

## 알고리즘/수식
**이미징 모델 (SOCS 기반):**
$$I(x) = \sum_k \sigma_k |h_k * m(x)|^2$$
여기서 $\sigma_k$는 소스 픽셀 강도, $h_k$는 부분 코히어런트 시스템의 커널, $m(x)$는 마스크 투과율.

**소스 최적화 목적함수 그래디언트:**
$$\frac{\partial F}{\partial \sigma_k} = \sum_x \frac{\partial F}{\partial I(x)} \cdot |h_k * m(x)|^2$$

**마스크 최적화 (sigmoid 모델):**
$$m(x) = \frac{1}{1 + e^{-\alpha \cdot z(x)}}$$
여기서 $z(x)$는 최적화 변수, $\alpha$는 경사도 파라미터.

**SMO 교번 반복:**
1. 현재 마스크 $m$으로 소스 $\sigma$ 최적화
2. 현재 소스 $\sigma$로 마스크 $m$ 최적화
3. 수렴까지 반복

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 모듈의 소스/마스크 교번 최적화 구조의 직접적 참고 자료
- 그래디언트 계산 방식: `skopc/smo/` 내 `source_optimizer.py` 및 `mask_optimizer.py` 구현 시 그래디언트 도출 공식 그대로 활용 가능
- 픽셀 기반 소스 표현 방식은 현재 SMO 구현의 기본 아키텍처와 일치
- SOCS 분해 기반 효율적 aerial image 계산은 TCC 행렬 고유값 분해와 등가

## 참고문헌 (핵심)
- Rosenbluth et al., "Optimum mask and source patterns to print a given shape," JM3 2002
- Ma & Arce, "Generalized inverse lithography methods for phase-shifting mask design," Optics Express 2007
- Pati & Kailath, "Phase-shifting masks for microlithography," JOSA A 1994

## 태그
`SMO`, `IEEE`, `gradient-based`, `source-optimization`, `mask-optimization`, `SOCS`, `193nm`, `pixel-based`, `optical-lithography`
