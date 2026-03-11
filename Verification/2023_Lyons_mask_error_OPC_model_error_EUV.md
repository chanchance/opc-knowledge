# Mask Error and Its Contribution to OPC Model Error for an EUV Via Layer

## 메타데이터
- **저자**: Adam Lyons, Tom Wallow, Chris Spence, Bríd Connolly, Christian Beurgel, Markus Bender
- **연도**: 2023
- **게재지**: Proc. SPIE 12750, International Conference on Extreme Ultraviolet Lithography 2023, 127500E
- **DOI/URL**: https://doi.org/10.1117/12.2687699

## 핵심 요약
EUV via 레이어에서 마스크 오차(mask error)가 OPC 모델 캘리브레이션 오차에 미치는 기여를 정량화한 논문. Tachyon 기반 플로우를 이용하여 1000개 OPC 모델 캘리브레이션 패턴에서 마스크 오차 체계(mask error systematics)를 측정하고, 이를 웨이퍼 수준으로 시뮬레이션하여 OPC 모델 잔차(residual)에 대한 마스크 오차의 기여 비중을 분리 정량화하였다.

## 주요 기여
1. **마스크 오차 체계 측정 플로우**: Tachyon 기반으로 1000개 캘리브레이션 패턴에서 마스크 오차 체계(systematic mask error)를 측정하는 방법론 수립
2. **웨이퍼 영향 시뮬레이션**: 측정된 마스크 오차를 웨이퍼 수준 CD 영향으로 변환하는 시뮬레이션 플로우
3. **OPC 모델 캘리브레이션 오차 분리**: 총 OPC 모델 캘리브레이션 오차에서 마스크 오차 기여분을 타 오차 소스(레지스트, 공정 변동)와 분리
4. **N5 EUV via 레이어 실증**: 5nm 기술 노드 EUV via 레이어에서 실제 데이터로 검증
5. **MEEF 보정을 포함한 통합 오차 예산**: 마스크 오차, MEEF, 공정 변동을 통합한 OPC 모델 오차 예산 프레임워크

## 검증 방법론
- 1000개 OPC 모델 캘리브레이션 패턴을 대상으로 마스크 CD 측정(CD-SEM 또는 e-beam mask inspection)
- Tachyon 시뮬레이터로 마스크 오차가 웨이퍼 CD에 미치는 영향 계산
- 마스크 오차 포함/제외 OPC 모델의 캘리브레이션 잔차(RMSE) 비교
- 마스크 오차 기여 비중(%) 정량화: 전체 모델 오차 대비 마스크 오차 비율

## OPC 툴 구현 관련성
- SKOPC 모델 캘리브레이션 모듈에서 마스크 오차를 독립 파라미터로 처리하는 설계 근거
- `2019_Chen_mask_process_correction_optical_weak_pattern.md`와 함께 마스크-OPC 오차 상호작용 이해의 핵심 논문 쌍
- `2005_Kim_MEEF_full_chip_model_based_verification.md`(기수집)의 MEEF 이론을 EUV 시대에 실증한 후속 연구
- OPC 모델 캘리브레이션 보고서에 마스크 오차 기여 항목을 포함하는 검증 표준 수립에 참조

## 태그
`Verification`, `SPIE`, `EUV`, `Mask Error`, `OPC Model`, `Calibration`, `MEEF`, `Via Layer`, `N5`
