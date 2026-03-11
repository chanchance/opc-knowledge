# Fast TCC Algorithm for the Model Building of High NA Lithography Simulation

## 메타데이터
- **저자**: Rosenbluth, A. E. et al. (IBM Research)
- **연도**: 2005
- **게재지**: Proc. SPIE 5754, Optical Microlithography XVIII
- **DOI/URL**: https://doi.org/10.1117/12.599591
- **인용수**: ~70

## 핵심 요약
고개구수(High NA) 리소그래피 시뮬레이션 모델 구축을 위한 빠른 TCC(Transmission Cross Coefficient) 계산 알고리즘을 제안한다. 렌즈 및 조명 퓨필 비트맵의 해상도를 높이면서도 합리적인 계산 속도를 유지하는 방법을 제시한다. Hopkins 편광 TCC의 고속 SVD(Singular Value Decomposition) 기반 커널 분해를 통해 OPC 모델 빌딩 속도를 크게 향상시킨다.

## 주요 기여
1. High NA(>0.9) 조건에서 편광 효과를 포함한 TCC 고속 계산법
2. 고해상도 퓨필 비트맵 처리를 위한 메모리/속도 최적화
3. SVD 기반 TCC 커널 분해의 수치 정확도 향상
4. 비-Kirchhoff 효과(벡터 회절) 포함 모델 빌딩 가이드라인
5. OPC 툴 통합을 위한 실용적 구현 전략

## 모델 수식/아키텍처

**Hopkins TCC (스칼라):**
```
TCC(f,g; f',g') = ∫∫ J(f₀,g₀) · H(f+f₀, g+g₀) · H*(f'+f₀, g'+g₀) df₀dg₀
```
여기서:
- J = 부분 가간섭 광원 분포 (Source)
- H = 렌즈 전달함수 (Pupil function)
- (f,g) = 주파수 좌표

**편광 TCC (벡터, High NA):**
```
TCC_pol(f,g; f',g') = Σ_{p=x,y,z} ∫∫ J(f₀) · H_p(f+f₀) · H_p*(f'+f₀) df₀
```
편광 성분 p ∈ {x, y, z} 각각에 대해 TCC 계산 후 합산

**SVD 커널 분해 (SOCS: Sum Of Coherent Sources):**
```
TCC(f,g; f',g') ≈ Σ_k λ_k · φ_k(f,g) · φ_k*(f',g')
```
- λ_k = k번째 고유값 (중요도 순 정렬)
- φ_k = k번째 고유함수 (coherent kernel)
- 상위 K개 항으로 절단하여 근사: K ~ 16~64개

**공중상 계산:**
```
I(x,y) = Σ_k λ_k · |∫∫ φ_k(f,g) · M(f,g) · e^{i2π(fx+gy)} df dg|²
```
M(f,g) = 마스크 스펙트럼

**계산 복잡도:**
- 기존: O(N_pupil⁴) → SVD 후: O(K · N_pupil²)
- K개 커널만 사용 시 ~10-100× 속도 향상

## 모델 유형
- [x] 광학 모델
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 모델 빌딩의 핵심: TCC → SVD → SOCS 커널 추출 파이프라인
- skopc/modeling/optical/ 구현 시 핵심 참조 논문
- High NA(immersion 1.35NA) 이상에서 편광 TCC 필수
- 커널 수 K 선택이 속도-정확도 트레이드오프 결정
- EUV(0.33NA → 0.55NA) 고NA 시대에도 동일 원리 적용

## 참고문헌
- Hopkins, H.H., "On the Diffraction Theory of Optical Images" (1953)
- Rosenbluth, A.E. et al., TCC decomposition papers (IBM)
- Cobb, N., "Fast Optical and Process Proximity Correction Algorithms" (1998)

## 태그
`Model`, `SPIE`, `OpticalModel`, `TCC`, `SVD`, `SOCS`, `KernelDecomposition`, `HighNA`, `2005`
