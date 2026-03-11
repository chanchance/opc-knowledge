# Reduced Basis Method for Source Mask Optimization

## 메타데이터
- **저자**: J. Pomplun, L. Zschiedrich, S. Burger, F. Schmidt, J. Tyminski, D. Flagello, N. Toshiharu
- **연도**: 2010
- **게재지/학회**: Proc. SPIE Vol. 7823, BACUS Photomask Technology 2010
- **DOI/URL**: https://doi.org/10.48550/arXiv.1011.2902 / https://arxiv.org/abs/1011.2902
- **인용수**: 다수 (SPIE 학회 논문)

## 핵심 요약
반도체 리소그래피에서 SMO(Source Mask Optimization)의 계산 비용을 극적으로 줄이기 위해 Reduced Basis Method(RBM)를 도입한 논문. 최적화 과정을 오프라인(모델 구축)과 온라인(빠른 풀이) 두 단계로 분리하여, 마스크 광투과 시뮬레이션의 계산 효율을 대폭 향상시킨다. 45nm 이하 노드에서 기존 SMO의 컴퓨팅 병목을 해결하는 핵심 접근법을 제시한다.

## 주요 기여
- 리소그래피 마스크 광투과 시뮬레이션에 RBM을 최초 적용하여 SMO 속도 향상
- 오프라인 단계에서 FEM(유한요소법) 기반 자기적응적 RBM 모델 구축
- 온라인 단계에서 임의의 조명/기하학적 파라미터에 대한 신속한 풀이 가능
- 엄격한 오차 추정기(rigorous error estimators)를 통한 솔루션 품질 보증
- 3D SMO 예제에 적용하여 정확도와 속도 간 최적 균형 실증

## 알고리즘/수식
- **Maxwell 방정식 기반**: 완전 벡터 Maxwell 방정식으로 마스크 광투과 특성 계산
- **오프라인 단계**: 가변 기하학적 파라미터에 대해 FEM으로 RBM 모델을 자기적응적으로 구축
  - Greedy 알고리즘으로 기저 함수(basis functions) 선택
  - 오차 추정기로 수렴 판단
- **온라인 단계**: 구축된 RBM 모델로 임의 파라미터에 대해 빠른 계산
  - 계산 복잡도: O(N_rb³) (N_rb << N_fe, 자유도 수)
- **SMO 적용**: 소스 픽셀과 마스크 파라미터를 결합 최적화

## OPC 툴 구현 관련성
SKOPC의 SMO 모듈에서 리소그래피 시뮬레이션 가속화에 직접 활용 가능. TorchLitho/LithoEngine의 forward 계산 속도를 높이기 위해 RBM 전처리 단계를 도입할 수 있음. 특히 반복적인 SMO 이터레이션에서 Maxwell 풀이를 RBM으로 대체하면 수십~수백 배의 속도 향상 가능. SKOPC의 `skopc/smo/` 모듈에서 LithoEngine 호출 최적화에 참고.

## 참고문헌 (핵심)
- Rosenbluth et al., "Optimum mask and source patterns to print a given shape," SPIE (2002)
-Granik, "Source optimization for image fidelity and telecentricity," JM3 (2004)
- JNI Pomplun et al., FEM-based lithography simulation tools (JCO 시리즈)

## 태그
`SMO`, `reduced-basis-method`, `RBM`, `FEM`, `Maxwell-equations`, `computational-lithography`, `mask-optimization`, `source-optimization`, `SPIE`, `2010`, `efficiency`
