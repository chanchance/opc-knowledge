# Neural Lithography: Close the Design-to-Manufacturing Gap in Computational Optics with a 'Real2Sim' Learned Photolithography Simulator

## 메타데이터
- **저자**: Cheng Zheng, Guangyuan Zhao, Peter So
- **연도**: 2023
- **게재지**: ACM SIGGRAPH Asia 2023 Conference Papers
- **DOI/URL**: https://doi.org/10.1145/3610548.3618251; arXiv:2309.17343
- **인용수**: ~40

## 핵심 요약
계산 광학 설계에서 '설계-제조 갭(design-to-manufacturing gap)'을 해소하는 완전 미분 가능 신경 리소그래피(Neural Lithography) 프레임워크를 제안한다. 실제 리소그래피 시스템을 Real2Sim 파이프라인으로 고충실도 신경 디지털 트윈(neural digital twin)으로 디지털화하고, 이 미분 가능 시뮬레이터를 모델 기반 광학 설계 루프에 통합하여 설계-제조 공동 최적화를 달성한다. 홀로그래픽 광학 소자(HOE)와 다중 레벨 회절 렌즈(MDL) 설계 및 제조에서 효과를 실증한다.

## 주요 기여
1. Real2Sim 파이프라인: 실제 리소그래피 시스템 → 고충실도 신경 디지털 트윈
2. 물리 기반 + 데이터 기반 혼합 리소그래피 시뮬레이터 (완전 미분 가능)
3. 설계-제조 공동 최적화: 리소그래피 시뮬레이터를 설계 최적화 루프에 통합
4. HOE, MDL 설계에서 설계-제조 갭 해소 실증

## Recipe/Process Flow 상세

### 설계-제조 갭 문제
```
계산 광학 설계의 현실:
  설계 최적화: 이상적 제조 가정 (설계 = 제조 결과)
  실제 리소그래피:
    회절 효과: 패턴 크기 축소/왜곡
    빔 프로파일: 비이상적 광원 형태
    포토레지스트: 노광-현상 비선형 반응
    기계 진동: 실제 패터닝 불균일

갭 결과:
  설계한 광학 소자 ≠ 제조된 광학 소자
  성능 편차: 설계 목표 달성 실패
  반복 재설계: 시행착오 증가

기존 해결 방법:
  수작업 보정: 경험 기반 프리컴프 → 부정확
  OPC: IC 제조에 특화, 계산 광학 직접 적용 어려움
  Neural Lithography: 범용 리소그래피 신경 시뮬레이터
```

### Real2Sim 파이프라인
```
목표: 실제 리소그래피 시스템 → 미분 가능 신경 모델

단계 1: 실험 데이터 수집
  테스트 패턴 세트 → 실제 리소그래피 패터닝
  결과 패턴: SEM 또는 광학 현미경으로 측정
  쌍 데이터: (설계 패턴, 제조 패턴)

단계 2: 물리 기반 베이스 모델
  Hopkins 광학 모델 + 레지스트 모델
  파라미터: NA, λ, 레지스트 파라미터
  기반 이미징 물리 표현

단계 3: 신경 보정 네트워크
  물리 모델 출력 → 신경망 보정
  실제 데이터로 훈련: 잔차 학습
  구조: ResNet/U-Net 기반 보정 레이어
  → 물리 모델 + 데이터 기반 보정 = 고충실도 시뮬레이터

미분 가능성:
  물리 모델: 해석적 → autograd 호환
  신경 보정: PyTorch → 자동 미분
  전체: ∂(제조 패턴)/∂(설계 파라미터) 계산 가능
```

### 설계-제조 공동 최적화
```
기존 설계 최적화:
  min_design ||ideal_target - ideal_sim(design)||²
  문제: ideal_sim ≠ real_litho → 설계-제조 갭

Neural Lithography 최적화:
  min_design ||target - neural_litho_sim(design)||²
  neural_litho_sim: 실제 리소그래피 시뮬레이터
  → 설계 → 실제 제조 결과 예측 → 목표와 비교 → 설계 업데이트

2단계 프레임워크:
  단계 1: 이상적 광학 설계 최적화
    (리소그래피 무시, 빠른 수렴)
  단계 2: 리소그래피 인식 미세 최적화
    neural_litho_sim 통합 → 제조 가능성 보정
    기울기: ∂(litho_loss)/∂(design) = autograd
```

### 적용 사례
```
홀로그래픽 광학 소자 (HOE):
  설계: 특정 회절 패턴
  리소그래피: 이중 광자 리소그래피 (2-photon)
  Neural Litho: 2-photon 리소그래피 디지털 트윈
  결과: 설계-제조 갭 크게 감소, 회절 효율 향상

다중 레벨 회절 렌즈 (MDL):
  설계: 다중 레벨 위상 프로파일
  리소그래피: 단계적 패터닝 프로세스
  결과: 제조 결함 감소, 렌즈 성능 향상

IC OPC와의 관계:
  Neural Lithography: 계산 광학 범용 접근
  IC OPC: IC 반도체 특화 (DUV/EUV, NA~0.33)
  공통: 미분 가능 리소그래피 시뮬 + 역최적화
  차이: IC OPC → 마스크 변형 / Neural Litho → 설계 변형
```

## OPC 툴 구현 관련성
- **SKOPC 미분 가능 시뮬**: Neural Lithography의 Real2Sim 개념을 SKOPC 리소그래피 모델 캘리브레이션에 활용
- **물리+데이터 혼합 모델**: TorchLitho에 신경 보정 레이어 추가 → 실제 공정 정확도 향상
- **설계-제조 갭**: IC OPC에서도 설계 → OPC 마스크 → 웨이퍼 갭 최소화에 동일 원리 적용
- **디지털 트윈**: 공정 캘리브레이션으로 생성된 신경 리소그래피 모델을 OPC 루프에 통합

## 참고문헌
- SIGGRAPH Asia 2023; arXiv:2309.17343
- 저자 소속: MIT (Peter So 그룹) + CUHK
- MIT News: https://news.mit.edu/2023/closing-design-manufacturing-gap-optical-devices-1213
- 관련: TorchLitho open-source differentiable (SPIE 2024)
- 관련: Neural-ILT (ICCAD 2020 / TCAD 2022)

## 태그
`Recipe`, `SIGGRAPH`, `NeuralLithography`, `Real2Sim`, `DigitalTwin`, `Differentiable`, `DesignManufacturing`, `ComputationalOptics`, `HOE`, `MIT`, `PhysicsInformed`, `2023`
