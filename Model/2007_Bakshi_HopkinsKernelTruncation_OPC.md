# Heuristics for Truncating the Number of Optical Kernels in Hopkins Image Calculations for Model-Based OPC Treatment

## 메타데이터
- **저자**: (SPIE 6520 발표, 2007)
- **연도**: 2007
- **게재지**: Proc. SPIE 6520, Optical Microlithography XX, 65203I
- **DOI/URL**: https://doi.org/10.1117/12.712625

## 핵심 요약
Hopkins 이미징 방정식의 광학 시스템 응답 함수를 특이값 분해(SVD)로 커널 집합으로 분해하고, 모델 기반 OPC 처리에서 최적 커널 수를 결정하는 휴리스틱 방법을 제안한다. 커널 수 축소로 시뮬레이션 속도를 높이면서 필요한 정확도를 유지한다.

## 주요 기여
1. Hopkins TCC(Transmission Cross Coefficient)를 SVD로 커널(eigenfunction) 집합으로 분해하는 방법
2. 부분 가간섭 광학 시스템을 가간섭 이미지의 합으로 표현하는 수학적 프레임워크
3. OPC 처리에서 정확도-속도 트레이드오프를 위한 최적 커널 수 결정 휴리스틱
4. 커널 수 축소에 따른 이미지 정확도 손실 정량화
5. 풀칩 OPC에서 실용적인 커널 수 선택 가이드라인 제공

## 모델 수식/아키텍처
- **Hopkins TCC**: TCC(f,g;f',g') = ∫∫ J(f-f₀, g-g₀) · K*(f-f₀, g-g₀) · K(f'-f₀, g'-g₀) df₀dg₀
- **SVD 분해**: TCC ≈ Σᵢ λᵢ · φᵢ(f,g) · φᵢ*(f',g')
- **이미지 계산**: I(x,y) ≈ Σᵢ |φᵢ(x,y) ⊗ mask(x,y)|²
- 커널 수 N: λᵢ/λ₁ < ε 조건으로 절단 (ε = 0.01~0.001)
- 커널 수 vs. 정확도 트레이드오프: N=20~50이 실용적 범위

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC LithoEngine의 Hopkins TCC 커널 수 최적화에 직접 적용
- 커널 수 자동 선택 알고리즘 구현 기반 제공
- OPC 런타임과 정확도 균형을 위한 핵심 이론적 기반
- TorchLitho 백엔드의 TCC 계산 최적화에도 적용 가능

## 태그
`Model`, `Optical`, `Hopkins`, `TCC`, `SVD`, `KernelDecomposition`, `OPC`, `Simulation`, `SPIE`
