# GPU-Accelerated Inverse Lithography Towards High Quality Curvy Mask Generation

## 메타데이터
- **저자**: Haoyu Yang, Haoxing Ren (NVIDIA Corp.)
- **연도**: 2024
- **게재지/학회**: arXiv:2411.07311
- **DOI/URL**: https://arxiv.org/html/2411.07311v1
- **인용수**: N/A (2024년 출판)

## 핵심 요약
CurvyILT는 multi-beam 마스크 작성기를 위한 ILT(역리소그래피 기술) 기반 포토마스크 설계 최적화 알고리즘이다. 커브형 설계 리타겟팅(CDR), 미분 가능 모폴로지 연산자, 푸리에 도메인 평활화 제약을 결합하여 마스크 윤곽 품질, 공정 창 견고성, 곡선형 정밀도를 향상시키면서 제조 복잡성을 줄인다. 기존 학술 솔버 대비 EPE 위반 30% 감소를 달성한다.

## 주요 기여
- **커브형 설계 리타겟팅(CDR)**: 폴리곤 모서리를 부드럽게 처리하여 달성 불가능한 목표의 과최적화를 줄이고 수렴 속도 향상
- **미분 가능 모폴로지 연산자**: 침식, 팽창, 열기, 닫기 연산을 최적화 중 미분 가능 함수로 구현하여 최적화 후가 아닌 중간에 아티팩트 제어
- **향상된 ILT 알고리즘**: CDR, 모폴로지 연산자, 푸리에 도메인 평활화 제약을 결합한 CurvyILT 솔버
- **우수한 성능**: 기존 학술 솔버 대비 EPE 위반 30% 감소 및 더 나은 공정 변동 밴드 유지

## Recipe/Process Flow 상세

### 3단계 핵심 프로세스

**전처리(Preprocessing)**
1. CDR(Curvilinear Design Retargeting) 적용으로 폴리곤 모서리 평활화
2. 초기 마스크 초기화
3. 달성 불가능한 목표 제거로 최적화 목적함수 개선

**최적화(Optimization)**
1. Hopkins 회절 모델을 사용한 리소그래피 시뮬레이션 실행
   - 레지스트 임계값 모델링으로 마스크 설계에서 항공 이미지 시뮬레이션
2. Adam 옵티마이저로 반복 마스크 개선
3. 미분 가능 모폴로지 연산자로 마스크 곡률 제어 및 아티팩트 제거
4. 공정 창 최적화 손실 함수 최소화:
   - 공칭 레지스트 불일치
   - 공정 변동 밴드 면적
   - 고주파 마스크 성분
5. SRAF는 명시적 제약 없이 최적화 과정에서 자연스럽게 생성

**후처리(Post-processing)**
1. 최종 마스크 업스케일
2. 이진화(Binarization)
3. 최종 마스크 품질 검증

### 손실 함수 구성
- 공칭 조건 정확도: 목표 패턴과의 레지스트 불일치
- 공정 변동 밴드(PVB) 면적: 제조 변동에 대한 견고성
- 고주파 마스크 성분: 제조 가능성 제어

### 평가 지표
- **EPEV**: EPE 위반 수 (기하학적 정확도)
- **PVB**: 공정 변동 밴드 면적 (견고성)
- **MSA**: 최소 형상 면적 (제조 가능성)
- **MSD**: 피처 간 최소 형상 거리

### 실험 결과
- ICCAD13 벤치마크: MultiILT 대비 평균 8.6% MSE 감소, EPE 위반 30% 감소
- LithoBench 데이터셋: EPE 위반 2× 개선, PVB 11% 감소
- 메모리 효율: 경쟁 방법 7.2GB 대비 0.6GB 피크 메모리

## OPC 툴 구현 관련성
- **ILT 엔진**: 커브형 마스크 생성을 지원하는 ILT 모듈 구현에 CurvyILT 알고리즘 직접 참조
- **공정 창 최적화 레시피**: PVB 기반 최적화 손실 함수를 레시피 파라미터로 노출하는 설계
- **SRAF 자동 생성**: 명시적 규칙 없이 최적화를 통해 SRAF가 자연 생성되는 원리 적용
- **모폴로지 후처리**: OPC 결과의 제조 가능성 향상을 위한 모폴로지 연산 파이프라인 구성
- **GPU 가속**: NVIDIA GPU 기반 ILT 엔진 구현 참조 (코드: github.com/phdyang007/curvyILT)

## 참고문헌 (핵심)
- Wang et al. (2022): A2-ILT - Spatial attention 기반 ILT
- Sun et al. (2023): Multi-level lithography simulation (기준 솔버)
- Wong et al. (2000): Mask error factor fundamentals
- Comer & Delp (1998): 모폴로지 연산 이론

## 태그
`CurvyILT`, `Inverse Lithography`, `GPU`, `CUDA`, `Process Window`, `SRAF`, `Morphological Operators`, `Curvilinear Mask`, `Recipe`, `OPC`, `Multi-beam Mask Writer`
