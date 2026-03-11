# Simultaneous Source Mask Optimization (SMO)

## 메타데이터
- **저자**: Robert Socha, Xuelong Shi, David LeHoty
- **연도**: 2005
- **게재지/학회**: Proc. SPIE 5853, Photomask and Next-Generation Lithography Mask Technology XII, pp. 180– (28 June 2005)
- **DOI/URL**: https://doi.org/10.1117/12.617431
- **인용수**: 매우 많음 (SMO 분야 창시 논문 중 하나)

## 핵심 요약
소스와 마스크를 동시에 최적화하여 공정 마진을 향상시키는 최초의 체계적인 동시 SMO 방법을 제안한다. 마스크를 주파수 도메인에서 최적화하고, 임계 패턴의 단편화 점(fragmentation points)에서 최소 이미지 로그 기울기(ILS)를 최대화하면서 프린팅 충실도를 유지한다. 주파수 도메인에서 최적화된 마스크는 크롬리스 위상 리소그래피(CPL) 마스크로 변환된다.

## 주요 기여
- 동시 소스-마스크 최적화(SMO)의 최초 체계적 방법론 제시
- 마스크를 주파수 도메인에서 최적화하여 ILS 최대화
- CPL(크롬리스 위상 리소그래피) 마스크와 최적화 소스 결합으로 공정 마진 2배 달성
- 간섭 매핑(interference mapping)을 이용한 전체 칩 나머지 부분 최적화 전략
- 피치 주파수 기반 전체 칩 소스 최적화 기법 제시

## 알고리즘/수식
**주파수 도메인 마스크 최적화:**
마스크 스펙트럼 $\hat{M}(f,g)$를 최적화 변수로 설정:
$$\max_{\hat{M}, \sigma} \quad \min_{j \in \text{fragmentation points}} ILS_j(\hat{M}, \sigma)$$

**ILS (이미지 로그 기울기):**
$$ILS = \frac{1}{I} \frac{dI}{dx}\bigg|_{edge}$$

**TCC 기반 이미징 (주파수 도메인):**
$$I(x) = \iint TCC(f_1,g_1;f_2,g_2) \hat{M}(f_1,g_1)\hat{M}^*(f_2,g_2) e^{2\pi i[(f_1-f_2)x]} df_1 df_2$$

**공정 마진 향상:**
- CPL 마스크 + 최적화 소스: aerial image 대비 2배 향상
- PSM + 소스 최적화만: 기준
- 동시 최적화: 공정 마진 2× 개선

**간섭 매핑 (Interference Mapping):**
전체 칩에서 임계 패턴 외 부분을 ILS 지도(interference map)로 평가하여 소스 재조정.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 모듈의 역사적 기반이 되는 창시 논문 - 설계 철학 이해에 필수
- 주파수 도메인 마스크 최적화 방식은 현재 ILT와 SMO 결합 구현 시 참고
- CPL 마스크 지원을 위한 마스크 타입 확장 시 참고
- 전체 칩 소스 최적화 전략(피치 주파수 기반)을 `skopc/smo/fullchip_smo.py`에 구현 가능

## 참고문헌 (핵심)
- Rosenbluth et al., "Optimum mask and source patterns," JM3 2002
- Granik, "Source optimization for image fidelity and throughput," JM3 2004
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008

## 태그
`SMO`, `SPIE`, `simultaneous-SMO`, `frequency-domain`, `CPL-mask`, `ILS`, `interference-mapping`, `process-window`, `chromeless-phase`, `foundational-paper`
