# Informational Lithography Approach Based on Source and Mask Optimization

## 메타데이터
- **저자**: Yihua Pan, Xu Ma, Shengen Zhang, Javier Garcia-Frias, Gonzalo R. Arce
- **연도**: 2021
- **게재지/학회**: IEEE Xplore (document 9311175); 관련 저널: Applied Optics, Vol. 60, No. 27, pp. 8307–8315 (2021)
- **DOI/URL**: https://ieeexplore.ieee.org/document/9311175/
- **인용수**: 확인 필요

## 핵심 요약
자유형 조명(freeform illumination) 구성에서 리소그래피 시스템의 정보 전달 메커니즘을 정보 이론 관점에서 분석하는 정보론적 리소그래피(informational lithography) 접근법을 제안한다. 소스-마스크 최적화를 채널 용량(channel capacity) 최대화 문제로 재공식화하여 SMO의 새로운 이론적 프레임워크를 제시한다. 정보 전달 효율을 높이는 최적 소스 형상 및 마스크 패턴을 도출한다.

## 주요 기여
- 리소그래피 이미징을 정보 채널(information channel)로 모델링하는 새로운 이론 프레임워크
- 자유형 조명 하에서의 정보 전달 메커니즘 해석
- SMO를 채널 용량 최대화로 재공식화
- 정보 이론 기반 소스 및 마스크 최적화 알고리즘 개발

## 알고리즘/수식
**리소그래피 채널 모델:**
$$I(x) = \mathcal{L}[\sigma, m](x) + n(x)$$
여기서 $\mathcal{L}$은 리소그래피 이미징 연산자, $n(x)$는 노이즈.

**채널 용량 기반 목적함수:**
$$\max_{\sigma, m} \quad C(\sigma, m) = I(X; Y|\sigma, m)$$
여기서 $I(X;Y)$는 입력 마스크 패턴 $X$와 출력 웨이퍼 이미지 $Y$ 간의 상호 정보량.

**상호 정보량:**
$$I(X;Y) = H(Y) - H(Y|X) = H(Y) - H(n)$$
노이즈 $n$이 고정이면 $H(Y)$ 최대화 → 출력 엔트로피 최대화.

**SOCS 기반 정보 채널:**
$$I(x) = \sum_k \sigma_k |h_k * m|^2$$
소스 픽셀 $\sigma_k$가 채널 가중치 역할.

**정보론적 SMO:**
$$\max_{\sigma \geq 0, m} H\left(\sum_k \sigma_k |h_k * m|^2\right)$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 소스 최적화 목적함수를 정보 이론 관점으로 확장할 때 참고
- 채널 용량 기반 소스 평가 지표를 `skopc/smo/metrics.py`에 추가 가능
- 자유형 조명 최적화의 이론적 상한(channel capacity bound) 계산에 활용
- EPE/공정 마진 외의 대안적 목적함수 설계에 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma & Arce, "Compressive lithography," Wiley 2023
- Cover & Thomas, "Elements of information theory," Wiley 2006

## 태그
`SMO`, `IEEE`, `information-theory`, `channel-capacity`, `mutual-information`, `informational-lithography`, `freeform-illumination`, `entropy`, `source-optimization`, `theoretical-framework`
