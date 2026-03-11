# Source-Mask Optimization (SMO): From Theory to Practice

## 메타데이터
- **저자**: Thuc Dam, Vikram Tolani, Peter Hu, Ki-Ho Baik, Linyong Pang, Bob Gleason, Steven D. Slonaker, Jacek K. Tyminski
- **연도**: 2010
- **게재지/학회**: Proc. SPIE 7640, Optical Microlithography XXIII, 764028 (3 March 2010)
- **DOI/URL**: https://doi.org/10.1117/12.848257
- **인용수**: 다수

## 핵심 요약
SMO의 이론적 기반을 실제 제조 환경에 적용하는 방법을 포괄적으로 다룬다. ASML FlexRay 조명기를 통한 자유형 조명(freeform illumination)을 포함하여 픽셀화 DOE 기반 소스와 복잡한 마스크 패턴의 동시 최적화를 22nm 노드 SRAM 컨택/메탈 레이어에 적용한다. SMO 결과물을 실제 스캐너에서 검증하는 전체 플로우를 제시한다.

## 주요 기여
- SMO 이론에서 실제 팹 적용까지의 완전한 플로우 제시
- 22nm 노드 SRAM 컨택 레이어 및 메탈 레이어에 SMO + 자유형 조명 적용 실증
- FlexRay(ASML 프로그래머블 조명기) 및 픽셀화 DOE 양쪽 조명 시스템 지원
- 하드 마스크에 전체 컨택/메탈 레이어 프린팅 시 SMO + 자유형 조명 효과 검증

## 알고리즘/수식
**SMO 최적화 목적함수 (공정 마진 최대화):**
$$\max_{\sigma, m} \quad \text{PW}(\sigma, m) = \min_j \text{EL}_j \times \text{DOF}_j$$

**SOCS 기반 부분 코히어런트 이미징:**
$$I(x) = \sum_{k=1}^{K} \sigma_k |f_k(x)|^2, \quad f_k(x) = h_k(x) * m(x)$$
여기서 $K$는 SOCS 항의 수 (상위 고유값만 사용하여 근사).

**소스 제약 조건 (FlexRay):**
$$\sigma \geq 0, \quad \sum_i \sigma_i = 1, \quad \sigma \in \mathcal{S}_{FlexRay}$$
$\mathcal{S}_{FlexRay}$: ASML 조명기 제조 가능성 제약 집합

**마스크 이진화:**
최적화 후 회색조 마스크를 이진 크롬/위상 전환 마스크로 변환:
$$m_{binary}(x) = \text{sign}(m_{opt}(x) - 0.5)$$

## OPC 툴 SMO 구현 관련성
- SKOPC의 SMO 플로우 설계 시 산업 표준 플로우 참고
- SOCS 항 수 $K$ 선택에 따른 정확도-속도 트레이드오프 기준 제시
- 자유형 소스를 실제 조명기 제약 조건에 맞게 양자화하는 방법 참고
- 22nm 노드 실제 적용 결과로 SMO 성능 벤치마크 기준 제공

## 참고문헌 (핵심)
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008
- Rosenbluth et al., "Optimum mask and source patterns," JM3 2002
- Socha et al., "Simultaneous source mask optimization," Proc. SPIE 5853, 2005

## 태그
`SMO`, `SPIE`, `freeform-illumination`, `FlexRay`, `22nm-node`, `SRAM`, `theory-to-practice`, `optical-microlithography`, `pixelated-source`, `process-window`
