# PRISM: Photonics-Informed Inverse Lithography for Manufacturable Inverse-Designed Photonic Integrated Circuits

## 메타데이터
- **저자**: Hongjian Zhou (Arizona State University), Haoyu Yang (NVIDIA), Nicholas Gangi, Tianle Xu (RPI), Rena Huang (RPI), Jiaqi Gu (ASU)
- **연도**: 2025
- **게재지/학회**: arXiv:2602.15762
- **DOI/URL**: https://arxiv.org/abs/2602.15762
- **인용수**: N/A (2025년 출판)

## 핵심 요약
PRISM은 포토닉 집적 회로(PIC)의 제조 가능성 격차를 해소하는 포토닉스 기반 역리소그래피 프레임워크다. (i) 최소한의 제조 데이터를 요구하는 컴팩트 캘리브레이션 패턴 합성, (ii) 그래디언트 기반 최적화를 가능하게 하는 물리 기반 미분 가능 제조 모델, (iii) 기하학 일치를 넘어 포토닉 기능을 우선시하는 포토닉스 기반 역 마스크 최적화로 구성된다. EBL 및 193nm DUV 리소그래피 모두에서 수율을 크게 향상시킨다.

## 주요 기여
- **캘리브레이션 패턴 합성**: 컴팩트한 정보량 있는 캘리브레이션 패턴으로 필요 제조 데이터 최소화
- **물리 기반 디지털 트윈**: 리소그래피 및 임계값 단계를 분해하는 인수분해 디지털 트윈
- **포토닉스 기반 역 리소그래피**: EM 필드 인식 목적 함수로 기하학 일치를 넘어 포토닉 기능 보존
- **종합 검증**: EBL 및 DUV 리소그래피 모두에서 수율 향상 및 캘리브레이션 오버헤드 감소 입증

## Recipe/Process Flow 상세

### PRISM 3기둥 프레임워크

**기둥 1: 캘리브레이션 패턴 합성**
세 가지 보완적 패턴 범주:
1. 일반 포토닉 기본 요소 (선, 굽힘, 테이퍼, 접합, 모듈레이터) - 해석 가능한 프로브
2. 다중 스케일 특성을 포함하는 제어된 전력 스펙트럼의 무작위 커브형 패턴
3. 분포 매칭을 위한 역 설계 장치 클롭

"가상 파운드리":
- DUV 포토리소그래피: SOCS Hopkins 이미징 모델 시뮬레이션
- EBL: 전자 산란 점 확산 함수 시뮬레이션

**기둥 2: 미분 가능 제조 디지털 트윈**
분해 모델: W = Φ_θ(M) = ψ(I_{θ_I}(M) - T_{θ_T}(M))
- I: 연속 노출 필드 생성 리소그래피 모듈
- T: 소프트 이진화를 통한 이진 마스크 생성 임계값 모듈

두 가지 구현:
- 데이터 기반: 다중 스케일 비국소 마스크-노출 매핑용 U-Net 백본
- 물리 기반: 학습 가능한 SOCS 커널(DUV, 12 Zernike 계수) 또는 이중 가우시안 PSF(EBL, 5 파라미터)

**기둥 3: 포토닉스 기반 역 리소그래피 알고리즘 (Algorithm 1)**
1. 잠재 레벨셋 변수로 최적화
2. 가우시안 스무딩 + 시그모이드 재파라미터화로 제조 가능성 강제
3. EM 필드 인식 손실 함수: L₄(W,W*) = ||Γ ⊙ (W-W*)||₄⁴
   - Γ: 성능 지표(FoM) 핵심 영역 강조 정규화 인접 민감도
4. 변동 인식 최적화: 마스크 보정 중 세 공정 코너(min/nominal/max) 샘플링

### DUV vs EBL 리소그래피 모델 차이

**DUV (193nm 포토리소그래피)**
- SOCS 기반 Hopkins 회절 이미징
- Zernike 수차 계수 (12개 학습 가능)
- 강한 광학 근접 효과로 수정 필요성 높음

**EBL (전자빔 리소그래피)**
- 이중 가우시안 PSF (5개 파라미터)
- 전자 후방 산란 효과
- 낮은 임계값 정확도로 근포화 메트릭

### 실험 결과

**EBL 결과 (10개 역 설계 장치)**
- 굽힘, 교차, 분배기, 모듈레이터: 80% 성능 임계값에서 100% 수율 달성
- WDM: 수율₈₀% 86% → 100% (ILT 후)

**DUV 결과**
- 비보정 WDM 전송: 0.973 → 0.215 (열화 심각)
- PRISM ILT 후 WDM 수율₈₀%: 0% → 54%
- Bragg 격자 수율₈₀%: ~0% → 90%

**FAID-ILT 시너지** (설계 영역 8μm², MFS 300nm)
- 보정 후: |S₂₁|² = 0.227 → 0.907

## OPC 툴 구현 관련성
- **포토닉 OPC 레시피**: 반도체 IC OPC와 유사하나 포토닉 PIC를 위한 EM 기능 보존 역 리소그래피 레시피 설계
- **물리 기반 캘리브레이션**: 소수의 제조 데이터로 OPC 공정 모델 캘리브레이션 - 반도체 OPC 레시피 캘리브레이션에 적용 가능
- **SOCS 학습 가능 커널**: OPC 레시피에서 Hopkins SOCS 파라미터를 웨이퍼 측정 데이터로 자동 캘리브레이션
- **변동 인식 OPC 레시피**: 공정 코너 3점(min/nominal/max) 샘플링으로 OPC 레시피 공정 변동 견고성 향상
- **레벨셋 역 리소그래피**: 레벨셋 변수 기반 OPC/ILT 최적화에 PRISM Algorithm 1 참조

## 참고문헌 (핵심)
- Yang & Ren (2024): CurvyILT (arXiv:2411.07311)
- Hopkins 회절 이미징 모델
- SOCS SVD 근사 방법
- 이중 가우시안 EBL PSF 모델
- FAID (제조 인식 역 설계) 관련 연구

## 태그
`PRISM`, `Photonic ILT`, `PIC`, `Inverse Lithography`, `EBL`, `DUV`, `SOCS`, `Differentiable Fabrication`, `Digital Twin`, `Level Set`, `Process Window`, `Recipe`, `OPC`, `Manufacturability`, `Yield Optimization`
