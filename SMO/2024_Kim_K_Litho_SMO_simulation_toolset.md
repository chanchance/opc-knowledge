# Development of a Lithography Simulation Tool Set in Various Optical Conditions for Source Mask Optimization

## 메타데이터
- **저자**: (IEEE Access 2024, document 10504808, 상세 저자 정보 확인 필요)
- **연도**: 2024
- **게재지/학회**: IEEE Access, DOI: 10.1109/ACCESS.2024.3390936
- **DOI/URL**: https://ieeexplore.ieee.org/document/10504808/
- **인용수**: 확인 필요

## 핵심 요약
광원 형상, 마스크 형상, 수치 개구(NA), 노출 파장 등 다양한 광학 조건을 사용자가 설정할 수 있는 리소그래피 시뮬레이션 툴셋(K-Litho)을 개발하였다. 오픈 리소그래피 시뮬레이션 툴의 부족 문제를 해결하며, SMO를 위한 다양한 광학 조건 시뮬레이션을 지원한다. ArF/EUV 등 다양한 파장 및 NA 조건에서 aerial image 계산, 레지스트 모델, 공정 마진 분석 기능을 포함한다.

## 주요 기여
- 다양한 광학 조건(파장, NA, 소스 형상)을 지원하는 오픈 리소그래피 시뮬레이션 툴셋 개발
- SMO를 위한 소스 형상 최적화 모듈 통합
- 기존 상업용 툴(Synopsys S-Litho, ASML Tachyon 등)의 오픈 대안 제공
- IEEE Access 게재로 재현 가능한 SMO 연구 환경 구축 기여

## 알고리즘/수식
**부분 코히어런트 이미징 (Hopkins 공식):**
$$I(x,y) = \iint TCC(f_1,g_1;f_2,g_2) \hat{M}(f_1,g_1) \hat{M}^*(f_2,g_2) e^{2\pi i [(f_1-f_2)x + (g_1-g_2)y]} df_1 dg_1 df_2 dg_2$$

**TCC (Transmission Cross Coefficient):**
$$TCC(f_1,g_1;f_2,g_2) = \iint J(f,g) H(f+f_1,g+g_1) H^*(f+f_2,g+g_2) df\, dg$$
여기서 $J(f,g)$는 소스 강도 분포, $H$는 투영 렌즈 전달 함수.

**SOCS 근사 (TCC 고유값 분해):**
$$TCC \approx \sum_{k=1}^{K} \lambda_k \phi_k(f_1,g_1) \phi_k^*(f_2,g_2)$$
상위 $K$개 고유값/고유벡터만 사용하여 계산 효율 향상.

**레지스트 모델 (임계값 기반):**
$$CD = \{x : I(x) = I_{th}\}$$

**SMO 연동 소스 최적화:**
소스 픽셀 강도 $J(f_k, g_k)$를 최적화 변수로 설정,
공정 마진(EL, DOF) 최대화 또는 EPE 최소화 목적함수 사용.

## OPC 툴 SMO 구현 관련성
- SKOPC 자체 리소그래피 시뮬레이션 엔진 구현 시 TCC/SOCS 공식 직접 참조
- K-Litho의 오픈소스 구조를 참고하여 `skopc/litho/` 모듈 설계 가능
- 다양한 파장/NA 조건 지원을 위한 모듈화 설계 방법 참고
- SMO와 시뮬레이션 엔진의 인터페이스 설계 참고

## 참고문헌 (핵심)
- Hopkins, "On the diffraction theory of optical images," Proc. Royal Society 1953
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Synopsys S-Litho, ASML Tachyon 상업용 툴 비교

## 태그
`SMO`, `IEEE`, `lithography-simulation`, `toolset`, `K-Litho`, `TCC`, `SOCS`, `Hopkins-formulation`, `open-source`, `optical-conditions`, `ArF`, `EUV`
