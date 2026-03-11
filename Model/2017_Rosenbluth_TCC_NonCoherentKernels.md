# Decomposition of the TCC Using Non-Coherent Kernels for Faster Calculation of Lithographic Images

## 메타데이터
- **저자**: Rosenbluth, A. E. et al. (IBM Research)
- **연도**: 2017
- **게재지**: Proc. SPIE 10147, Optical Microlithography XXX
- **DOI/URL**: https://doi.org/10.1117/12.2261223
- **인용수**: ~25

## 핵심 요약
리소그래피 이미지 계산 가속화를 위한 TCC의 비간섭(non-coherent) 커널 분해 방법을 제안한다. 기존 SOCS(Sum of Coherent Sources) 분해가 포착하기 어려운 TCC의 Toeplitz 근방 성분을 비간섭 구조로 효율적으로 표현한다. 렌즈 날카로운 애퍼처에 의한 불연속성(slope discontinuities)에서 발생하는 near-Toeplitz 성분에 특히 효과적이다.

## 주요 기여
1. TCC 비간섭 커널 분해라는 새로운 분해 방식 제안
2. 렌즈 애퍼처 불연속성 처리: 기존 SVD 분해 대비 수렴 속도 향상
3. near-Toeplitz TCC 성분의 공간 도메인 효율적 처리
4. 복합 시스템(compound systems)을 활용한 목표 TCC 성분 추출
5. 전체 TCC에 대한 최소자승 최적 근사 달성

## 모델 수식/아키텍처

**기존 SOCS (Coherent 분해):**
```
TCC(f,g; f',g') ≈ Σ_k λ_k · φ_k(f,g) · φ_k*(f',g')
```
λ_k, φ_k: SVD 고유값/고유함수 (간섭성 커널)

**Non-Coherent 커널 분해 (신규):**
```
TCC(f,g; f',g') ≈ Σ_j w_j · |K_j(f-f', g-g')|²
```
K_j = j번째 비간섭 커널 (공간 도메인 컨볼루션 형태)
w_j = 양의 가중치

**Toeplitz 근방 성분:**
```
TCC_Toeplitz(f,g; f',g') ≈ TCC(f-f₀, g-g₀)   [위치 이동 불변 근사]
```
날카로운 애퍼처 경계에서 이 근사가 깨짐 → non-coherent 커널로 보정

**최소자승 최적화:**
```
min_{w_j, K_j} ||TCC_exact - Σ_j w_j|K_j|²||²_F
subject to: w_j ≥ 0   [비간섭성 조건]
```

**계산 이득:**
```
이미지 계산: I(x) = Σ_j w_j · |K_j * M(x)|²
M(x) = 마스크 함수, * = 컨볼루션
→ 커널 수 J << SOCS 커널 수 K로 동일 정확도 달성
```

## 모델 유형
- [x] 광학 모델
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 모델 빌딩 광학 계산 가속화에 직접 적용 가능
- skopc/modeling/optical/tcc.py 에서 비간섭 커널 옵션 추가
- 특히 High Contrast 애퍼처(원형, 고리형 조명) 처리에 유리
- 기존 SOCS 대비 적은 커널 수로 동일 정확도 → OPC 런타임 단축
- EUV 편광 TCC에도 동일 원리 적용 가능

## 참고문헌
- Hopkins, H.H., "On the Diffraction Theory of Optical Images" (1953)
- Rosenbluth, A.E. et al., "Fast TCC algorithm for High NA" (2005)
- Cobb, N., "Fast optical and process proximity correction" (1998)

## 태그
`Model`, `SPIE`, `OpticalModel`, `TCC`, `NonCoherentKernels`, `KernelDecomposition`, `SOCS`, `LithographySimulation`, `2017`
