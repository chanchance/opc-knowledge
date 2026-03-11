# Optimum Mask and Source Patterns to Print a Given Shape

## 메타데이터
- **저자**: Alan E. Rosenbluth, Scott J. Bukofsky, Carlos A. Fonseca, Michael S. Hibbs, Kafai Lai, Antoinette F. Molless, Rama Nand Singh, Alfred K. K. Wong
- **연도**: 2002
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS and MOEMS (JM3), Vol. 1, No. 1 (1 April 2002)
- **DOI/URL**: https://doi.org/10.1117/1.1448500
- **인용수**: 매우 많음 (SMO 분야 원조 논문, 수백 인용)

## 핵심 요약
SMO(Source Mask Optimization) 분야의 창시 논문. 소스가 조정 가능할 때 마스크 형상에 새로운 자유도가 추가되며, 필요한 이미지 대칭성을 마스크 대신 소스에서 제공할 수 있음을 보인다. 타겟 패턴과 매우 다른 새로운 마스크 형상 집합이 최적해가 될 수 있으므로, 타겟 패턴을 시작점으로 쓰지 않는 좋은 전역 수렴성을 가진 알고리즘을 개발한다. 표준 RET 대비 2~6배 큰 공정 마진을 달성한다.

## 주요 기여
- 소스와 마스크를 동시 최적화하는 SMO 개념 최초 정립 (IBM Research)
- 타겟 패턴과 무관하게 전역 수렴하는 최적화 알고리즘 개발
- 위상 전환(phase shift) 마스크 + 최적화 소스 조합으로 공정 마진 2~6× 향상
- 트림 마스크(trim mask) 불필요한 새로운 마스크 형상 도출

## 알고리즘/수식
**최적화 문제 공식화:**
$$\max_{\sigma, m} \quad PW(\sigma, m)$$
subject to: 소스 강도 비음수 $\sigma \geq 0$, 마스크 물리적 제약

**부분 코히어런트 이미징:**
$$I(x) = \iint TCC(f_1,g_1;f_2,g_2) \hat{M}(f_1,g_1)\hat{M}^*(f_2,g_2) e^{2\pi i[(f_1-f_2)x+(g_1-g_2)y]} d\mathbf{f}_1 d\mathbf{f}_2$$

**TCC와 소스의 관계:**
$$TCC(f_1,g_1;f_2,g_2) = \iint J(f,g) H(f+f_1,g+g_1) H^*(f+f_2,g+g_2) df\, dg$$
소스 $J$를 변경하면 전체 TCC가 변함 → 소스 최적화가 마스크 최적화 자유도에 영향.

**전역 최적화 알고리즘:**
- 시작점 독립적(start-design-free) 전역 탐색
- 위상 전환 마스크 포함한 복소 마스크 최적화
- 공정 마진(ED window 면적) 최대화

**공정 마진 정의 (E-D 윈도우):**
$$PW = \text{Area}\{(E, f) : |CD(E,f) - CD_{target}| \leq \Delta CD_{spec}\}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 모듈 전체의 이론적 기반 - 반드시 읽어야 할 창시 논문
- TCC와 소스의 관계 공식은 `skopc/litho/tcc.py` 구현의 수학적 근거
- 전역 최적화 알고리즘 설계 시 출발점 독립성의 중요성 인식
- E-D 윈도우 기반 공정 마진 정의는 `skopc/smo/metrics.py`의 기준

## 참고문헌 (핵심)
- Hopkins, "On the diffraction theory of optical images," Proc. Royal Society 1953
- Levenson et al., "Improving resolution in photolithography with a phase-shifting mask," IEEE TED 1982
- Wong & Neureuther, "Mask topography effects in projection printing," IEEE TED 1994

## 태그
`SMO`, `SPIE`, `JM3`, `foundational-paper`, `IBM-Research`, `Rosenbluth`, `global-optimization`, `phase-shift-mask`, `TCC`, `process-window`, `E-D-window`, `start-design-free`
