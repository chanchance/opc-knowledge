# SMO for 28-nm Logic Device and Beyond: Impact of Source and Mask Complexity on Lithography Performance

## 메타데이터
- **저자**: Seiji Nagahara, Kazuyuki Yoshimochi, Hiroshi Yamazaki, Kazuhiro Takeda, Takayuki Uchiyama, Stephen Hsu, Zhipan Li, Hua-yu Liu, Keith Gronlund, Terunobu Kurosawa, Jun Ye, Luoqi Chen, Hong Chen, Zheng Li, Xiaofeng Liu, Wei Liu
- **연도**: 2010
- **게재지/학회**: Proc. SPIE 7640, Optical Microlithography XXIII, 76401H (2010)
- **DOI/URL**: https://doi.org/10.1117/12.846473
- **인용수**: 다수

## 핵심 요약
28nm 로직 소자를 위한 SMO 적용을 체계적으로 연구하며 소스 복잡도와 마스크 복잡도가 리소그래피 성능에 미치는 영향을 정량화한다. 프로그래머블 조명기(FlexRay)와 표준 DOE를 비교하고, SRAF 구성과 MRC(마스크 규칙 검사) 기준을 변화시켜 다양한 마스크 복잡도 SMO를 비교한다. 리소그래피 성능과 소스/마스크 복잡도 간 균형에 기반한 비용 효율적 생산 접근법을 제시한다.

## 주요 기여
- 28nm 로직 소자에서 소스 복잡도(DOE vs. FlexRay)와 마스크 복잡도(SRAF, MRC)의 영향 체계적 정량화
- 다양한 k1 값에서 공정 마진 및 MEEF 평가
- 마스크 제조 가능성 및 마스크 쓰기 시간 분석
- 리소그래피 성능-소스/마스크 복잡도 트레이드오프에 기반한 비용 효율적 SMO 전략 제시

## 알고리즘/수식
**소스 복잡도 비교:**
- 표준 DOE: 제한적 형상 (annular, quasar, dipole 등)
- FlexRay: 픽셀 단위 자유형 소스, 거의 무제한 조명 분포

**마스크 복잡도 수준:**
1. 레벨 1: 기본 OPC만 (어시스트 피처 없음)
2. 레벨 2: 규칙 기반 SRAF + OPC
3. 레벨 3: 최적화된 SRAF + OPC
4. 레벨 4: SMO + 최적화 SRAF + ILT

**k1 인자와 공정 마진:**
$$k_1 = \frac{CD \cdot NA}{\lambda}$$
낮은 k1일수록 더 높은 소스/마스크 복잡도 SMO 필요.

**SMO 성능 지표:**
$$\text{Score} = EL(\%) \times DOF(\mu m) / MEEF^2$$
소스/마스크 복잡도 증가에 따른 Score 향상 대비 비용 증가 분석.

**마스크 쓰기 시간 모델:**
$$T_{write} \propto N_{shapes} \cdot A_{total}$$
복잡한 마스크(ILT 결과)는 형상 수 급증으로 쓰기 시간 증가.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 모듈 설계 시 소스/마스크 복잡도 수준별 SMO 플로우 구성 참고
- FlexRay vs. DOE 소스 타입별 SMO 결과 비교로 조명기 타입 선택 기준 제공
- SRAF와 SMO 통합 플로우 (`skopc/smo/sraf_smo.py`) 설계의 직접 참고
- 비용-성능 트레이드오프 분석 방법론 참고

## 참고문헌 (핵심)
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008
- Dam et al., "SMO from theory to practice," Proc. SPIE 7640, 2010
- Rosenbluth et al., "Intensive optimization for 22nm," Proc. SPIE 7274, 2009

## 태그
`SMO`, `SPIE`, `28nm-node`, `logic-device`, `source-complexity`, `mask-complexity`, `DOE`, `FlexRay`, `SRAF`, `MRC`, `k1-factor`, `MEEF`, `mask-write-time`, `cost-performance-tradeoff`
