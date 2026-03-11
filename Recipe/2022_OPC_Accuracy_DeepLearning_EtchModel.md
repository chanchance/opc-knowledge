# OPC Accuracy Improvement Through Deep-Learning Based Etch Model

## 메타데이터
- **저자**: (SPIE 12056 - 2022 SPIE Advanced Lithography)
- **연도**: 2022
- **게재지**: Proc. SPIE 12056, Metrology, Inspection, and Process Control XXXVI
- **DOI/URL**: https://doi.org/10.1117/12.2613926
- **인용수**: ~20

## 핵심 요약
딥러닝 기반 식각 모델(Newron etch)을 DUV 리소-식각 공정에 통합한 풀칩 OPC 보정 흐름을 실증한다. SEM 계측과 자동화 계측 소프트웨어를 활용하여 대용량 식각 바이어스 데이터를 수집하고, 딥러닝 모델로 식각 모델을 캘리브레이션한다. 테스트 패턴에서 <50%, 실제 칩 패턴에서 <35%의 모델 캘리브레이션 오차 개선을 달성하며, OPC 정확도 향상을 검증한다.

## 주요 기여
1. Newron 딥러닝 식각 모델의 풀칩 OPC 흐름 통합 실증
2. 자동화 SEM 계측 소프트웨어로 대용량 식각 바이어스 데이터 수집
3. 테스트/실제 칩 패턴에서 식각 모델 정확도 50%/35% 개선
4. DUV 리소-식각 공정에서 OPC 최종 CD 정확도 향상

## Recipe/Process Flow 상세

### Newron 딥러닝 식각 모델
```
Newron etch 모델의 특징:
  - 딥러닝 기반 식각 바이어스 예측기
  - 입력: 패턴 기하학 피처 + 주변 밀도
  - 출력: 식각 바이어스 (ΔCD_etch)
  - 신경망 구조: 다층 완전연결 또는 CNN

기존 해석적 식각 모델과 차이:
  해석적 모델: 단순 파라미터 수식
    ΔCD_etch = a + b × CD + c × density
    장점: 빠름, 해석 가능
    단점: 복잡한 2D 패턴, 고차 효과 누락

  Newron 딥러닝 모델: 데이터 구동
    ΔCD_etch = DNN(CD, pitch, density, pattern features)
    장점: 복잡한 의존성 학습, 높은 정확도
    단점: 대용량 훈련 데이터 필요
```

### 자동화 계측 기반 데이터 수집
```
데이터 수집 파이프라인:
  1. 식각 테스트 패턴 설계
     - 다양한 CD (50-500nm)
     - 다양한 pitch (100nm-수 μm)
     - 다양한 패턴 밀도
     - 1D 및 2D 패턴 (코너, 끝단)

  2. 리소그래피 후 + 식각 후 SEM 측정
     자동화 계측 소프트웨어:
       - 대용량 자동 레시피 생성
       - 자동 이미지 취득 및 CD 추출
       - 수만 개 측정 포인트 처리

  3. 식각 바이어스 계산
     ΔCD_etch = CD_after_etch - CD_after_litho
     각 패턴에서 자동 계산

  4. 딥러닝 모델 훈련
     입력: 패턴 피처 벡터
     출력: ΔCD_etch
     훈련: Adam 최적화, MSE 손실
```

### 풀칩 OPC 흐름 통합
```
식각 인식 OPC 흐름:

단계 1: 식각 보상 타겟 계산
  Silicon target → Newron etch 예측 → Litho target
  Litho_target = Silicon_target - ΔCD_etch_predicted

단계 2: 표준 OPC 실행
  Litho_target → OPC → 마스크 패턴
  OPC 모델: 리소그래피 컴팩트 모델 (식각 미포함)

단계 3: 식각 후 검증
  마스크 → 리소그래피 시뮬 → CD_litho
  CD_litho + Newron etch → CD_final 예측
  CD_final vs. Silicon_target → 최종 EPE

단계 4: 반복 (필요 시)
  EPE가 크면: 식각 보상 타겟 재계산 → OPC 재실행
```

### 성능 결과 (DUV 리소-식각 공정)
```
모델 캘리브레이션 정확도:
  기존 해석적 식각 모델 대비 Newron 딥러닝:
    테스트 패턴: 캘리브레이션 오차 <50% 개선
    실제 칩 패턴: 캘리브레이션 오차 <35% 개선
  식각 바이어스 예측 RMS: 감소

OPC 최종 CD 정확도:
  Newron 식각 모델 통합 OPC:
    최종 CD 오차(EPE): 기존 대비 감소
  특히 밀도 변화가 큰 패턴에서 개선 두드러짐

풀칩 적용:
  런타임: 딥러닝 추론 overhead 허용 가능 수준
  대용량 칩 패턴에서 일관된 개선
```

## OPC 툴 구현 관련성
- **SKOPC Newron 식각 모델 통합**: `skopc/modeling/etch_model.py`에 딥러닝 식각 바이어스 예측기 구현
- **자동화 계측 데이터**: 외부 SEM 계측 데이터를 자동으로 파싱하여 모델 훈련 데이터 생성
- **OPC 타겟 보정**: OPC 실행 전 Newron 식각 모델로 리소그래피 타겟 자동 조정
- **풀칩 검증**: OPC 후 식각 시뮬레이션으로 최종 CD 예측 및 검증 자동화

## 참고문헌
- Proc. SPIE 12056, Metrology, Inspection, and Process Control XXXVI (2022)
- 관련: Using ML etch models in OPC and ILT correction (SPIE 11614, 2021)
- 관련: Accurate etch modeling with massive metrology and deep learning (SPIE 11327, 2020)
- 관련: Etch proximity correction through ML-driven etch bias model (SPIE 9782, 2016)

## 태그
`Recipe`, `SPIE`, `EtchModel`, `DeepLearning`, `Newron`, `OPC-Accuracy`, `EtchBias`, `AutomatedMetrology`, `DUV`, `FullChip`, `2022`
