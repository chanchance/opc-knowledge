# NXE:3400 OPC Process Monitoring: Model Validity vs Process Variability

## 메타데이터
- **저자**: Dongbo Xu, David Rio, Werner Gillijns, Max Delorme, Christina Baerts (imec)
- **연도**: 2021
- **게재지**: Proc. SPIE 11609, Extreme Ultraviolet (EUV) Lithography XII, 116091N
- **DOI/URL**: https://doi.org/10.1117/12.2583870

## 핵심 요약
imec N7 M2 레이어(피치 32nm)에서 ASML NXE:3400 EUV 스캐너와 공정 변동이 OPC 모델 정확도에 미치는 장기적 영향을 정량화하고, 도즈 튜닝을 통해 OPC 모델 유효성을 복원하는 능력을 평가한 논문. OPC 모델 정확도가 공정 제어 품질에 강하게 의존하며, 공정 변동을 무시하면 EPE 예산이 초과될 수 있음을 실증하였다.

## 주요 기여
1. **장기 OPC 모델 유효성 모니터링**: NXE:3400 스캐너 및 공정 변동 환경에서 OPC 모델의 장기 유효성 추적
2. **공정 변동의 OPC 정확도 영향 정량화**: 스캐너 변동(포커스, 도즈)과 공정 변동이 OPC 모델 EPE 예산에 미치는 기여 분리 정량화
3. **OPC 모델 도즈 튜닝 보정**: 공정 변동으로 손상된 OPC 모델 유효성을 도즈 파라미터 조정으로 복원하는 방법
4. **EUV 양산 환경 실증**: imec N7 M2 레이어 실제 양산 환경에서의 검증
5. **OPC 프로세스 모니터링 체계**: OPC 모델 유효성을 지속적으로 모니터링하는 체계적 플로우 제안

## 검증 방법론
- NXE:3400 스캐너 장기 운영 데이터(도즈, 포커스 변동)를 OPC 모델 검증 데이터와 매칭
- 공정 변동 발생 전후 OPC 모델 EPE 잔차(RMSE) 추이 분석
- 도즈 튜닝 적용 전후 OPC 모델 정확도 비교 (복원 효과 정량화)
- imec N7 M2 레이어 32nm 피치에서의 CD-SEM 측정 기반 검증

## OPC 툴 구현 관련성
- SKOPC의 OPC 모델 유효성 모니터링 기능 설계 시 핵심 참조 (모델 드리프트 감지 알고리즘)
- EUV 스캐너 운영 데이터와 OPC 모델 정확도 연동 모니터링 파이프라인 구현의 기반
- `2019_Ho_OPC_model_building_EUV_lithography.md`의 EUV OPC 모델 구축 이후 장기 운영 검증의 후속 연구
- SKOPC 레시피 시스템에서 공정 변동 감지 시 자동 도즈 조정 기능(adaptive dose tuning) 구현 근거

## 태그
`Verification`, `SPIE`, `EUV`, `OPC Model`, `Process Monitoring`, `NXE3400`, `Model Validity`, `Process Variability`, `Dose Tuning`, `imec`
