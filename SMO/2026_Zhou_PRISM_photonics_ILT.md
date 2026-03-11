# PRISM: Photonics-Informed Inverse Lithography for Manufacturable Inverse-Designed Photonic Integrated Circuits

## 메타데이터
- **저자**: Hongjian Zhou, Haoyu Yang, Nicholas Gangi, Tianle Xu, Rena Huang, Jiaqi Gu
- **연도**: 2026
- **게재지/학회**: arXiv:2602.15762 (physics.optics / cs.ET)
- **DOI/URL**: https://doi.org/10.48550/arXiv.2602.15762
- **인용수**: 신규 논문

## 핵심 요약
포토닉 집적회로(PIC, Photonic Integrated Circuit) 역설계의 제조 민감도 문제를 해결하는 PRISM(Photonics-Informed Inverse Lithography) 워크플로우를 제시한 논문. 시뮬레이션 설계와 실제 제조 소자 간의 성능 편차를 줄이기 위해, 캘리브레이션 패턴 합성, 물리 기반 미분가능 제조 모델, 광학 인식 마스크 최적화를 결합한다. 전자빔 리소그래피(EBL)와 심자외선(DUV) 포토리소그래피 모두에서 검증된 데이터 효율적 접근법.

## 주요 기여
- 컴팩트 캘리브레이션 패턴 합성으로 최소 제조 데이터로 모델 구축 (데이터 효율성)
- 물리 기반 그래디언트 계산 가능 제조 모델 개발 (미분가능 제조 시뮬레이터)
- 광학적으로 중요한 특징 우선화하는 포토닉스 인식 마스크 최적화 (단순 기하 매칭 초월)
- EBL + DUV 리소그래피 모두 지원하는 범용 워크플로우
- 제조 후 성능 및 수율(yield) 향상, 캘리브레이션 면적 및 개발 시간 절감

## 알고리즘/수식
- **미분가능 제조 모델**:
  - 리소그래피 공정을 미분가능 함수 F_litho로 모델링
  - 제조 패턴: m_fab = F_litho(m_design; θ)  (θ: 공정 파라미터)
  - 그래디언트: ∂L/∂m_design = ∂L/∂m_fab · ∂F_litho/∂m_design

- **포토닉스 인식 최적화**:
  ```
  min_{m} L_photonics(F_litho(m)) + λ·L_geometry(m)
  ```
  - L_photonics: 광학 성능 손실 (투과율, 반사율 등)
  - L_geometry: 기하 매칭 손실

- **캘리브레이션 패턴 합성**:
  - 정보 이득 최대화 기준으로 컴팩트 테스트 패턴 선택
  - 적은 측정 데이터로 F_litho 모델 파라미터 θ 추정

- **Hopkins 회절 모델 + 식각 모델**:
  - 리소그래피: Hopkins 부분 간섭 모델
  - 식각: 그래디언트 추정 기반 식각 모델 (BOSON-1 방식)

## OPC 툴 구현 관련성
SKOPC의 포토닉 소자 지원(미래 확장)에 참고. 현재 SKOPC가 반도체 IC 리소그래피 중심이지만, PIC 분야로 확장 시 이 워크플로우가 핵심 참조가 됨. 미분가능 제조 모델 개념은 SKOPC의 LithoEngine 캘리브레이션(`skopc/modeling/calibration.py`)에 적용 가능. 물리 기반 미분가능 시뮬레이터 구조는 범용적으로 참조.

## 참고문헌 (핵심)
- Yang & Ren, GPU-ILT (2024) — 공동저자 Haoyu Yang의 선행 연구
- BOSON-1: Hopkins + 식각 모델 역설계
- Inverse design 관련: adjoint method 원전들

## 태그
`PIC`, `photonic-integrated-circuit`, `inverse-lithography`, `differentiable`, `fabrication-model`, `calibration`, `EBL`, `DUV`, `mask-optimization`, `2026`, `arxiv`
