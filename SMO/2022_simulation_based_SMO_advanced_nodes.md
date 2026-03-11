# Simulation-Based Source and Mask Optimization for Advanced Nodes

## 메타데이터
- **저자**: (IEEE Xplore document 9856865, 상세 저자 정보 IEEE Xplore 직접 확인 필요)
- **연도**: 2022
- **게재지/학회**: IEEE Conference Publication (IEEE Xplore document 9856865)
- **DOI/URL**: https://ieeexplore.ieee.org/document/9856865/
- **인용수**: 확인 필요

## 핵심 요약
고급 노드(advanced node)를 위한 시뮬레이션 기반 소스-마스크 최적화(SMO) 방법을 제안한다. 소스의 동공 조명 효율(pupil illumination efficiency)을 타깃 패턴 기반으로 최적화하며, 포커스를 통한 도즈 허용 오차(dose latitude through focus)의 균형을 개선한다. SMO가 리소그래피 한계를 밀어내는 유망한 기술로서 고급 반도체 노드에의 적용 가능성을 제시한다.

## 주요 기여
- 고급 노드 대상 시뮬레이션 기반 SMO 플로우 제시
- 동공 조명 효율(pupil illumination efficiency) 최적화를 SMO 목적함수에 통합
- 포커스 변화에 따른 도즈 허용 오차 균형 개선 전략
- 실제 고급 노드 패턴에 대한 SMO 적용 결과 실증

## 알고리즘/수식
**동공 조명 효율 기반 소스 최적화:**
$$\eta_{pupil}(\sigma) = \frac{\sum_k \sigma_k \cdot w_k^{target}}{\sum_k \sigma_k}$$
여기서 $w_k^{target}$는 타깃 패턴에 대한 동공 픽셀 $k$의 기여 가중치.

**도즈 허용 오차-포커스 균형 목적함수:**
$$F = \alpha \cdot F_{EL}(\sigma, m) + \beta \cdot F_{DOF}(\sigma, m) + \gamma \cdot F_{MEEF}(\sigma, m)$$

**시뮬레이션 기반 SMO 플로우:**
1. 타깃 패턴 클립 추출
2. 광학 시뮬레이션 (SOCS 기반 aerial image)
3. 소스 최적화 (동공 효율 최대화)
4. 마스크 최적화 (ILT 또는 룰 기반 OPC)
5. 검증 시뮬레이션 및 반복

## OPC 툴 SMO 구현 관련성
- SKOPC의 시뮬레이션 기반 SMO 플로우 설계에 직접 참고
- 동공 조명 효율 계산을 `skopc/smo/pupil_efficiency.py`로 구현 가능
- 고급 노드(7nm 이하) SMO 적용 시나리오의 벤치마크 자료
- 도즈/포커스 균형 목적함수 구성 방법 참고

## 참고문헌 (핵심)
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008
- Liu et al., "EUV SMO for 7nm node and beyond," Proc. SPIE 9048, 2014
- Peng et al., "Gradient-based SMO," IEEE TIP 2011

## 태그
`SMO`, `IEEE`, `simulation-based`, `advanced-nodes`, `pupil-illumination-efficiency`, `dose-latitude`, `depth-of-focus`, `process-window`, `computational-lithography`
