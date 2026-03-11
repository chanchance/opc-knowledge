# Source Mask Optimization (SMO) Study for High-NA EUV Lithography to Achieve Single Patterning on Random Logic Metal

## 메타데이터
- **저자**: Soobin Hwang, Werner Gillijns, Stefan de Gendt, Ryoung-han Kim
- **연도**: 2024
- **게재지/학회**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540X (10 April 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010869
- **인용수**: 확인 필요

## 핵심 요약
고-NA EUV 리소그래피에서 단일 패터닝(single patterning)을 통한 랜덤 로직 메탈 스케일링 가능성을 SMO로 평가한다. 최소 피치 24, 22, 20nm 수평 방향 로직 메탈 디자인에 대해 8가지 마스크 조합(다크필드/브라이트필드, Ta 기반/저-n 위상 전환, SRAF 포함/제외)에서 SMO 성능을 체계적으로 비교한다. 공정 마진(process window)을 각 설계 변수 조합에 대해 정량 평가한다.

## 주요 기여
- 고-NA EUV 단일 패터닝 가능성을 SMO 관점에서 체계적 검증
- 8가지 마스크 타입 조합(다크/브라이트필드 × Ta/저-n PSM × SRAF 유무)의 SMO 성능 비교
- 24/22/20nm 피치 로직 메탈 패턴에 대한 공정 마진 정량 분석
- 고-NA EUV용 최적 마스크 타입 선정 기준 제시

## 알고리즘/수식
**고-NA EUV 이미징 모델:**
$$I(x) = \sum_k \sigma_k |h_k^{high-NA}(x) * m_{3D}(x)|^2$$
여기서 $h_k^{high-NA}$는 0.55 NA EUV 시스템 커널 (anamorphic 배율 4×8 포함).

**마스크 타입별 투과율/반사율 모델:**
- 다크필드: $r_{BG} \approx 0$ (흡수층 배경), $r_{open} = r_{MoSi}$
- 밝기필드: $r_{BG} = r_{MoSi}$ (반사층 배경), $r_{open} \approx 0$
- 저-n PSM: $r = |r|e^{i\phi}$, $\phi \neq 0$ (위상 전환)

**SMO 공정 마진 목적함수:**
$$\max_{\sigma, m} \quad PW = \{(CD_{err}, f) : |CD_{err}| \leq \Delta CD_{spec}\}$$

**SRAF 최적화:**
서브 해상도 어시스트 피처 위치/크기를 SMO와 동시 최적화:
$$\min_{\sigma, m, \{AF_i\}} EPE_{rms} + \lambda_{SRAF} \cdot N_{SRAF}$$

## OPC 툴 SMO 구현 관련성
- SKOPC의 고-NA EUV SMO 기능 구현 시 마스크 타입 선정 기준 제공
- `skopc/smo/euv_smo.py`에서 anamorphic 고-NA 광학계 모델링 참고
- 다크/브라이트필드 마스크 타입별 SMO 설정 방법 참고
- SRAF와 SMO의 동시 최적화 플로우 설계에 활용

## 참고문헌 (핵심)
- Liu et al., "EUV SMO for 7nm node and beyond," Proc. SPIE 9048, 2014
- Ma et al., "Gradient-based SMO for EUV," IEEE TCI 2019
- Zhao et al., "Computational lithography for EUV high-NA patterning," Proc. SPIE 12495, 2023

## 태그
`SMO`, `SPIE`, `high-NA-EUV`, `single-patterning`, `logic-metal`, `dark-field`, `bright-field`, `Ta-mask`, `low-n-PSM`, `SRAF`, `20nm-pitch`, `anamorphic`
