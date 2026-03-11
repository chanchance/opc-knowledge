# Differentiable Edge-based OPC

## 메타데이터
- **저자**: Guojin Chen, Haoyu Yang, Haoxing Ren, Bei Yu, David Z. Pan
- **연도**: 2024
- **게재지/학회**: ICCAD 2024 (IEEE/ACM International Conference on Computer-Aided Design)
- **DOI/URL**: https://arxiv.org/abs/2408.08969
- **인용수**: N/A (2024년 출판)

## 핵심 요약
DiffOPC는 edge-based OPC와 ILT(Inverse Lithography Technology)의 장점을 결합한 차별화된 OPC 프레임워크다. CUDA 가속 ray casting을 통한 효율적인 레이아웃 래스터화와 마스크 규칙 인식 경사 기반 최적화를 통해 기존 방법 대비 EPE(Edge Placement Error)를 낮추면서 제조 비용을 50% 절감한다. 마스크 경계까지 비용 함수의 그래디언트를 역전파하여 진정한 그래디언트 유도 최적화를 실현한다.

## 주요 기여
- **하이브리드 프레임워크**: pixel-based ILT의 유연성과 edge-based OPC의 제조 가능성을 결합
- **마스크 규칙 인식 최적화**: 제조 제약 조건을 준수하는 그래디언트 기반 접근법
- **비용 절감**: 기존 최신 기술 대비 제조 비용 50% 감소
- **MRC-clean 결과**: 후처리 없이 직접 마스크 제조에 사용 가능한 결과 생성
- **SRAF 배치 자동화**: 그래디언트를 활용한 최적 SRAF 배치 및 추가 최적화

## Recipe/Process Flow 상세

### 5단계 순방향 패스 알고리즘

**1단계: Edge 파라미터 반올림**
- Straight-Through Estimator(STE)를 사용한 에지 파라미터 반올림
- 이산 마스크 표현을 유지하면서 연속 최적화 공간 허용

**2단계: 모서리 에지 병합**
- 세그먼트 재연결을 위한 모서리 에지 병합
- 마스크 규칙 검사(MRC) 준수를 위해 과도하게 짧은 세그먼트 병합

**3단계: Edge-to-Mask 래스터화**
- CUDA 가속 ray casting을 통한 병렬화된 래스터화
- Manhattan 정렬 세그먼트 추출
- 병렬 격자점 교차 테스트
- 이진 마스크 생성을 위한 홀수-짝수 규칙 적용

**4단계: 순방향 리소그래피 시뮬레이션**
- SOCS(Sum of Coherent Systems) 분해를 사용한 항공 이미지 강도 계산
- I(x,y) ≈ Σ σᵢ|M(x,y) ⊗ hᵢ(x,y)|²
- 상수 임계값 레지스트 모델로 강도를 이진 레지스트 패턴으로 변환

**5단계: 손실 계산**
- EPE(Edge Placement Error): 기하학적 왜곡 측정
- L2 손실: 설계-인쇄 충실도
- PVB(Process Variation Band): ±2% 공정 조건에서의 견고성
- Shot Count: 제조 가능성 측정

### 그래디언트 계산 알고리즘
- 세그먼트 방향에 수직인 속도 벡터
- 중점 그래디언트 보간
- 래스터화를 통한 연쇄 규칙 미분

### SRAF 배치 프로세스
1. 그래디언트 정보를 활용한 최적 SRAF 시드 생성
2. 휴리스틱 방법 대신 체계적인 보조 피처 위치 지정
3. 최적화 프레임워크 내에서 추가 최적화 실행

## OPC 툴 구현 관련성
- **DiffOPC 프레임워크**: edge-based OPC 엔진의 핵심 최적화 루프 구현에 직접 활용 가능
- **SRAF 자동 삽입**: 레시피 실행 시 SRAF 배치 자동화 모듈 구현에 적용
- **MRC 통합**: 마스크 규칙 검사와 OPC 최적화를 단일 루프로 통합하는 방법론
- **CUDA 가속**: GPU 가속 래스터화 엔진 구현 참조
- **공정 변동 대응**: PVB 기반 프로세스 윈도우 최적화 레시피 설계

## 참고문헌 (핵심)
- Yang et al. (2018): GAN-OPC - Mask Optimization with Lithography-guided GANs
- Chen et al. (2021): DevelSet - Deep Neural Level Set for mask optimization
- Sun et al. (2023): Multi-level lithography simulation baseline
- Wong et al. (2000): Mask error factor fundamentals

## 태그
`DiffOPC`, `Edge-based OPC`, `ILT`, `CUDA`, `SRAF`, `MRC`, `Process Window`, `Recipe`, `OPC`, `Gradient Optimization`, `ICCAD2024`
