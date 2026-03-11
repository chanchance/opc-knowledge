# Integrated Mask Process Modeling for Better Yield Predictions

## 메타데이터
- **저자**: A. Awad, C. Behroozi, A. Erdmann
- **연도**: 2024
- **게재지**: Proc. SPIE 13216, Photomask Technology + EUV Lithography 2024, 132161W (20 November 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3035191

## 핵심 요약
마스크 제조 공정의 왜곡을 모델링하여 수율 예측 정확도를 향상시키는 통합 마스크 공정 모델링 방법을 제시한다. 기존 리소그래피 시뮬레이션이 마스크 제조를 이상적 공정으로 가정하는 한계를 극복하여, 마스크 제조 공정 왜곡을 포함한 종단간(end-to-end) 최적화를 가능하게 하는 미분 가능한 "화이트박스" 모델을 개발한다.

## 주요 기여
1. **통합 마스크 공정 모델**: 마스크 제조 왜곡을 포함한 종단간 리소그래피 모델
2. **미분 가능한 화이트박스 모델**: 블랙박스 방식 대비 해석 가능하고 최적화 가능한 모델
3. **수율 예측 향상**: 마스크 공정 변동 포함으로 실제 웨이퍼 수율 예측 정확도 향상
4. **설계 제조 용이성(DFM)**: 종단간 최적화로 마스크 제조 공정까지 고려한 OPC/ILT

## 알고리즘/수식
### 통합 마스크 공정 모델
```
기존 리소그래피 모델:
  I_wafer = Litho_sim(M_ideal)
  M_ideal: 이상적 마스크 (제조 공정 왜곡 없음)
  → 현실과 차이 → 수율 예측 오차

통합 마스크 공정 모델:
  M_real = MaskProcess(M_design)
  I_wafer = Litho_sim(M_real)

  MaskProcess: 마스크 제조 공정 모델
    - e-beam 노출 근접 효과 (MPC 보정 전후)
    - 에칭 후 CD 변화
    - 마스크 CD 균일성 변동

미분 가능한 화이트박스 모델:
  MaskProcess_diff(M_design): 미분 가능 → 그래디언트 역전파 가능
  → OPC/ILT 최적화에서 마스크 제조 단계 포함 최적화
```

### 종단간 최적화
```
종단간 OPC 최적화:
  min_M Cost(I_wafer(M_real(M_design)))
  = min_M Cost(Litho_sim(MaskProcess(M_design)))

  그래디언트:
  ∂Cost/∂M_design = ∂Cost/∂I_wafer · ∂I_wafer/∂M_real · ∂M_real/∂M_design
  → 마스크 제조 단계까지 역전파 가능

SEM 이미지 활용:
  제조된 마스크의 SEM 이미지 → 래스터 포맷 변환
  → 미분 가능한 픽셀 손실 함수 계산
```

## OPC 툴 SMO 구현 관련성
- 마스크 제조 인식 OPC: SKOPC OPC/SMO에서 마스크 공정 모델 통합
- 종단간 SMO: 웨이퍼 패턴부터 마스크 제조까지 포함한 SMO 비용 함수
- DFM 최적화: 마스크 제조 변동에 강건한 OPC/SMO 설계
- 수율 예측 개선: 마스크 공정 변동 포함으로 수율 시뮬레이션 정확도 향상

## 태그
`OPC`, `EUV`, `mask_process_modeling`, `yield_prediction`, `differentiable`, `end_to_end`, `DFM`, `mask_manufacturing`, `SPIE`, `2024`
