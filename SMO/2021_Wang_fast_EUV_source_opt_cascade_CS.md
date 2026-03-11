# Fast EUV Lithography Source Optimization Using Cascade Compressed Sensing

## 메타데이터
- **저자**: Zhiqiang Wang, Xu Ma, Rui Chen, Gonzalo R. Arce (추정, IEEE document 9601250)
- **연도**: 2021
- **게재지/학회**: IEEE Transactions on Computational Imaging (IEEE document 9601250)
- **DOI/URL**: https://ieeexplore.ieee.org/document/9601250/
- **인용수**: 확인 필요

## 핵심 요약
마스크 클립 라이브러리에 새 레이아웃 데이터가 추가될 때 최적 소스 패턴을 재계산해야 하는 중복 계산 문제를 해결하는 캐스케이드 압축 센싱 기반 EUV 소스 최적화(CCS-SO) 방법을 제안한다. 기존에 최적화된 소스 정보를 재활용하여 새 클립 추가 시 소스 최적화 계산을 대폭 가속화하며, EUV 리소그래피의 두꺼운 마스크 모델(thick mask model)도 지원한다.

## 주요 기여
- 마스크 클립 라이브러리 갱신 시 소스 재최적화 계산 비용 문제 해결
- 캐스케이드 CS 구조: 이전 최적화 결과를 다음 최적화의 웜스타트로 활용
- EUV thick mask model을 지원하는 소스 최적화 프레임워크
- 클립 라이브러리 점진적 확장 시나리오에서 대폭적인 속도 향상 실증

## 알고리즘/수식
**클립 라이브러리 기반 소스 최적화 문제:**
$N$개의 마스크 클립 $\{m_1, ..., m_N\}$에 대해 공통 소스 $\sigma$ 최적화:
$$\min_{\sigma \geq 0} \sum_{i=1}^{N} F_i(I_i(\sigma, m_i))$$

**캐스케이드 CS (CCS) 접근법:**
클립 $m_{N+1}$ 추가 시, 기존 해 $\sigma^*_N$을 초기값으로:
$$\min_{\sigma \geq 0} \sum_{i=1}^{N+1} F_i(\mathbf{A}_i \sigma) \approx \min_{\sigma \geq 0} \|\sigma - \sigma^*_N\|_{W}^2 + F_{N+1}(\mathbf{A}_{N+1} \sigma)$$
여기서 $W$는 이전 최적화에서 추출한 가중치 행렬.

**EUV Thick Mask 모델 통합:**
$$I(x) = \sum_k \sigma_k |h_k^{thick}(x) * m_{3D}(x)|^2$$
여기서 $h_k^{thick}$는 EUV 반사 마스크의 회절을 RCWA 또는 Kirchhoff 근사로 계산한 커널.

**CS 소스 복원:**
$$\min_{\sigma} \|\mathbf{A}\sigma - b_{target}\|_2^2 + \lambda\|\sigma\|_1 \quad \text{s.t.} \quad \sigma \geq 0$$
캐스케이드 구조로 새 클립 추가 시 전체 재최적화 불필요.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 다중 클립 동시 소스 최적화 구현 시 핵심 참고
- `skopc/smo/multi_clip_optimizer.py` 구현 시 CCS 알고리즘 적용 가능
- EUV thick mask 모델을 TorchLitho와 연동하는 방법의 이론적 기반
- 클립 라이브러리 점진적 확장 시나리오(온라인 학습 방식) 지원 아키텍처 설계 참고

## 참고문헌 (핵심)
- Wang et al., "Fast pixelated SMO based on compressive sensing," IEEE TASE 2020
- Ma et al., "Gradient-based SMO for EUV," IEEE TCI 2019
- Ma & Arce, "Compressive lithography: computational imaging for semiconductor lithography," Wiley 2023

## 태그
`SMO`, `IEEE`, `EUV`, `compressive-sensing`, `cascade-CS`, `source-optimization`, `clip-library`, `thick-mask-model`, `fast-optimization`, `incremental-update`
