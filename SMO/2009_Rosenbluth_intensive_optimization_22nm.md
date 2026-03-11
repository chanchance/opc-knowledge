# Intensive Optimization of Masks and Sources for 22nm Lithography

## 메타데이터
- **저자**: Alan E. Rosenbluth, David O. Melville, Kehan Tian, Saeed Bagheri, Jaione Tirapu-Azpiroz, Kafai Lai, Andreas Waechter, Tadanobu Inoue, Laszlo Ladanyi, Francisco Barahona, Katya Scheinberg, Masaharu Sakamoto, Hidemasa Muta, Emily Gallagher, Tom Faure, Michael Hibbs, Alexander Tritchkov, Yuri Granik
- **연도**: 2009
- **게재지/학회**: Proc. SPIE 7274, Optical Microlithography XXII, 727409 (16 March 2009)
- **DOI/URL**: https://doi.org/10.1117/12.814844
- **인용수**: 매우 많음 (22nm SMO 분야 핵심 논문)

## 핵심 요약
22nm 리소그래피를 위한 집중적인(intensive) 마스크 및 소스 최적화 방법을 제안한다. SMO는 비선형·비볼록 최적화 문제임을 분석하고, 전역 최적화 방법(마스크-소스 순차 최적화)과 마스크·소스 변수를 함께 다루는 로컬 결합 최적화를 모두 활용한다. 22nm SRAM 및 로직 패턴에 적용하여 기존 RET 대비 크게 향상된 공정 마진을 달성한다.

## 주요 기여
- SMO의 비선형·비볼록 특성 분석 및 전역-로컬 결합 최적화 전략 개발
- 전역 최적화 방법과 로컬 결합 최적화(마스크+소스 변수 동시)를 혼합 활용
- 22nm SRAM 및 로직 레이어에서 집중 SMO 적용 결과 실증
- IBM Research 팀의 대규모 협력 결과물 (SMO 분야 종합 논문)

## 알고리즘/수식
**SMO 최적화 문제의 비볼록성:**
$$\min_{\sigma, m} F(\sigma, m) \quad \text{(비볼록, 다중 로컬 미니마 존재)}$$

**전역 최적화 (순차):**
1. 소스 고정 → 마스크 전역 최적화 (ILT)
2. 마스크 고정 → 소스 전역 최적화 (LP 또는 컨벡스 완화)
3. 반복

**로컬 결합 최적화:**
마스크와 소스를 단일 벡터 $\mathbf{x} = [\sigma; m]$으로 묶어 동시 그래디언트 업데이트:
$$\mathbf{x}^{(t+1)} = \mathbf{x}^{(t)} - \mu \nabla_\mathbf{x} F(\mathbf{x}^{(t)})$$

**집중 SMO 전략:**
1. 전역 소스 최적화 (로컬 미니마 회피)
2. 전역 ILT 마스크 최적화
3. 로컬 결합 정밀화 (joint gradient)
4. 마스크 이진화 및 검증

**공정 마진 목적함수:**
$$\max_{\sigma, m} \quad \text{Effy}(\sigma, m) = \int\!\!\int_{PW} dE \, df$$
E-D 윈도우 면적(Effy = exposure-defocus window area) 최대화.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 모듈에서 전역+로컬 결합 최적화 전략 설계의 직접 참고
- 22nm 노드 실제 SRAM/로직 패턴 적용 결과로 SMO 성능 벤치마크 제공
- E-D 윈도우(Effy) 기반 목적함수 구현의 수학적 정의 제공
- 결합 마스크-소스 그래디언트 업데이트 방법 참고

## 참고문헌 (핵심)
- Rosenbluth et al., "Optimum mask and source patterns," JM3 2002
- Rosenbluth & Seong, "Global optimization of illumination," Proc. SPIE 2006
- Socha et al., "Simultaneous SMO," Proc. SPIE 5853, 2005

## 태그
`SMO`, `SPIE`, `IBM-Research`, `Rosenbluth`, `22nm-node`, `intensive-optimization`, `non-convex`, `global-local-optimization`, `ILT`, `SRAM`, `logic`, `E-D-window`, `joint-gradient`
