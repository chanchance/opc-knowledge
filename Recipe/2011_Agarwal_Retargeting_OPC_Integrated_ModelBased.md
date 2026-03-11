# Integrated Model-Based Retargeting and Optical Proximity Correction

## 메타데이터
- **저자**: Kanak B. Agarwal, Shayak Banerjee
- **연도**: 2011
- **게재지**: Proc. SPIE 7974, Design for Manufacturability through Design-Process Integration V, 79740F
- **DOI/URL**: https://doi.org/10.1117/12.879531

## 핵심 요약
기존의 룰 기반 retargeting은 기술 스케일링에 따라 커버할 수 없는 2D 형상 조합이 방대해져 확장성이 없다. 본 논문은 retargeting과 OPC를 통합하여 동시에 수행하는 모델 기반 접근법을 제안한다. 이미지 기울기(image slope) 정보를 리소그래피 공정 창의 척도로 사용하여, NILS가 낮은 fragment에 대해 동적으로 target을 수정하면서 OPC를 진행한다.

## 주요 기여
1. **통합 Retargeting-OPC**: retargeting과 OPC를 분리된 2단계가 아닌 단일 통합 플로우로 수행
2. **NILS 기반 타겟 수정**: 낮은 NILS를 갖는 fragment를 식별하여 OPC 반복 중 동적으로 타겟 조정
3. **저레벨 메탈 레이어 최적화**: M1 등 저레벨 금속 레이어의 리소그래피 수율 향상
4. **확장성**: 룰 기반 retargeting이 커버 못 하는 2D 형상에도 적용 가능

## Recipe/Flow 상세
- **통합 Retargeting-OPC 플로우**:
  1. **초기 타겟 설정**: 설계 레이아웃에서 OPC 초기 타겟 추출
  2. **OPC 시뮬레이션**: 현재 마스크 → 웨이퍼 이미지 시뮬레이션
  3. **NILS 계산**: 각 fragment 위치에서 Normalized Image Log Slope 계산
  4. **저-NILS fragment 식별**: NILS < 임계값인 fragment 선별
  5. **동적 타겟 수정**: 저-NILS fragment의 타겟을 image slope 방향으로 이동
     - 공정 창 개선 방향으로 타겟 재설정
  6. **OPC 업데이트**: 수정된 타겟으로 마스크 형상 업데이트
  7. **수렴 판정**: EPE 및 NILS 기준 만족 시 종료
- **대상 레이어**: 저레벨 금속 배선 (M1, M2)
- **핵심 메트릭**: NILS, EPE, 공정 창 (DOF × EL)
- **룰 기반 대비 장점**: 임의 2D 형상에 모델 기반으로 자동 적용 가능

## OPC 툴 구현 관련성
- OPC 수렴 루프에 retargeting 단계 통합하는 구조 참고
- NILS 계산 후 저-NILS fragment 동적 타겟 수정 로직
- `model_based_opc.py`: fragment NILS 평가 → 타겟 재조정 → OPC 업데이트 루프
- process window 개선을 위한 target modification 전략

## 태그
`Retargeting`, `OPC`, `ModelBased`, `NILS`, `ProcessWindow`, `MetalLayer`, `SPIE`, `2011`
