# Machine Learning-Based Edge Placement Error Analysis and Optimization: A Systematic Review

## 메타데이터
- **저자**: Anh Tuan Ngo, Bappaditya Dey, Sandip Halder et al.
- **연도**: 2022 (Epub 2022 Oct 26, 게재 2023 Feb)
- **게재지**: IEEE Transactions on Semiconductor Manufacturing, Vol. 36, No. 1, pp. 1–13
- **DOI/URL**: https://doi.org/10.1109/TSM.2022.3217326 (IEEE Xplore: 9930860)
- **인용수**: 다수 (EPE ML 리뷰 분야 주요 논문)

## 핵심 요약
반도체 제조 공정이 3nm 노드로 진입하면서 EPE(Edge Placement Error) 저감이 IC 소자 정상 동작을 위한 핵심 과제가 되었다. EPE는 멀티 패터닝 공정에서 패턴 충실도를 정량화하는 가장 중요한 지표로, 오버레이 오차와 CD 오차의 합성이다. 본 체계적 리뷰는 EPE 저감을 위한 ML/DL 적용 연구들을 가상 오버레이 계측, 오버레이 오차 저감, 마스크 최적화 세 범주로 체계적으로 정리한다.

## 주요 기여
1. EPE 분석·최적화에 ML/DL을 적용한 연구의 최초 체계적 리뷰 — 3nm 노드까지의 기술 동향 정리
2. 세 범주(가상 오버레이 계측, 오버레이 저감, 마스크 최적화) 별 ML 방법론 비교 분석
3. 각 연구의 목적, 데이터셋, 입력 피처, 모델, 주요 결과, 한계점 체계적 정리
4. EPE 최소화를 위한 미래 연구 방향 및 과제 도출

## 검증 방법론
- **EPE 정의 및 분해**:
  - `EPE_total = EPE_overlay + EPE_CD`
  - 오버레이 EPE: 레이어 간 정렬 오차에 의한 엣지 위치 편차
  - CD EPE: OPC 오차·리소그래피 변동에 의한 CD 오차 기여분
- **ML 기반 가상 계측**: SEM 이미지 없이 공정 파라미터로부터 오버레이·CD 예측
- **마스크 최적화 기반 EPE 저감**: CNN/GAN 기반 OPC로 EPE를 직접 최소화
- **평가 기준**: 예측 정확도(RMSE, MAE), EPE 저감률, 모델 일반화 성능
- **리뷰 방법론**: 체계적 문헌 검색 + 포함/제외 기준 적용 + 정성·정량 비교

## 검증 지표
- EPE 허용 범위: 3nm 노드 타겟 — 총 EPE 수 nm 이내 (오버레이 < 1nm, CD 오차 < 1nm 수준)
- 시뮬레이터: 각 리뷰 대상 논문별 다양 (SEM 계측, 리소그래피 시뮬레이터 등)
- 커버리지: 2015~2022년 발표 EPE 관련 ML 논문 망라

## OPC 툴 구현 관련성
- **EPE 기반 OPC 검증 모듈 설계의 종합 참조**: EPE 분해(오버레이 + CD 기여분) 구조를 `VerificationEngine` EPE 계산 모듈에 직접 적용 가능
- ML 기반 가상 계측으로 OPC 검증 시 계측 비용 없이 EPE 예측하는 파이프라인 구현 근거
- EPE 허용 기준(budget) 설정 방법론 및 3nm 이하 노드 대응 EPE 스펙 참고 자료
- 마스크 최적화 관점의 EPE 최소화 알고리즘을 OPC 수렴 기준으로 활용하는 설계 방향 제시

## 참고문헌
- IEEE Transactions on Semiconductor Manufacturing 2023, Vol. 36, No. 1
- Heriot-Watt University Research Portal 수록 (open access)

## 태그
`Verification`, `IEEE`, `EPE`, `EdgePlacementError`, `MachineLearning`, `SystematicReview`, `Overlay`, `CDControl`, `MaskOptimization`, `3nm`
