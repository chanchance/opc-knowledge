# Efficient Informatics-Based Source and Mask Optimization for Optical Lithography

## 메타데이터
- **저자**: Yihua Pan, Xu Ma, Shengen Zhang, Javier Garcia-Frias, Gonzalo R. Arce
- **연도**: 2021
- **게재지/학회**: Applied Optics, Vol. 60, No. 27, pp. 8307–8315
- **DOI/URL**: https://doi.org/10.1364/AO.433962
- **인용수**: 확인 필요

## 핵심 요약
리소그래피 시스템에서 정보 전달 메커니즘을 묘사하는 통신 채널 모델을 수립하여 효율적인 정보학 기반 SMO(EISMO) 방법을 개발한다. 그래디언트 기반 SMO 알고리즘으로 소스를 먼저 최적화한 후, 상호 정보량(mutual information)을 최대화하는 제조 인식(manufacturing-aware) 마스크 분포를 최적화하여 기존 SMO 대비 우수한 이미징 성능을 달성한다.

## 주요 기여
- 리소그래피를 통신 채널로 모델링하는 정보학적 SMO 프레임워크(EISMO) 제안
- 상호 정보량 최대화 기반 마스크 분포 최적화
- 제조 가능성을 고려한(manufacturing-aware) 마스크 설계
- 기존 그래디언트 기반 SMO 대비 계산 효율 및 이미징 성능 향상

## 알고리즘/수식
**통신 채널 모델 (리소그래피):**
$$I_{wafer}(x) = \mathcal{H}[\boldsymbol{\sigma}, m](x) + n(x)$$
마스크 $m$과 소스 $\boldsymbol{\sigma}$를 채널, $n$은 잡음.

**상호 정보량 기반 마스크 목적함수:**
$$\max_m I(M_{target}; I_{wafer}) = H(M_{target}) - H(M_{target} | I_{wafer})$$
목표 패턴 $M_{target}$과 웨이퍼 이미지 $I_{wafer}$ 간 상호 정보량 최대화.

**EISMO 2단계 알고리즘:**
```
단계 1: 그래디언트 기반 소스 최적화
  σ* = argmin_σ F_EPE(σ, m_init)

단계 2: 상호 정보량 기반 마스크 최적화
  m* = argmax_m I(M_target; I_wafer(σ*, m))
```

**제조 인식 마스크 분포:**
$$p(m) \propto \exp\left(-\lambda_{mfg} \cdot C_{mfg}(m)\right)$$
제조 비용 함수 $C_{mfg}$를 마스크 확률 분포에 통합.

**효율적 계산 (그래디언트 근사):**
$$\frac{\partial I(M_{target}; I_{wafer})}{\partial m} \approx \frac{\partial F_{EPE}}{\partial m} + \lambda_{info} \frac{\partial \log p(m)}{\partial m}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 정보학적 비용함수 설계 시 참고
- `skopc/smo/informatics_smo.py`에 통신 채널 모델 기반 EISMO 구현
- Pan et al. 2021 정보학적 리소그래피 SMO와 함께 정보 이론 SMO 계열로 참고
- 상호 정보량 기반 마스크 최적화는 마스크 제조 가능성과 자연스럽게 통합

## 참고문헌 (핵심)
- Pan et al., "Informational lithography SMO," IEEE/Applied Optics 2021
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "Pixelated SMO immersion," JOSAA 2013

## 태그
`SMO`, `Applied-Optics`, `informatics`, `mutual-information`, `communication-channel`, `manufacturing-aware`, `EISMO`, `information-theory`, `gradient-based`, `mask-distribution`
