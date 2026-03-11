# OPC Accuracy Improvement Through Deep-Learning Based Etch Model

## 메타데이터
- **저자**: Weina Shi, Liang Zhu, Yuqian Chen, Jiao Huang, Jinze Wang, Qian Xie, Bilun Zhang, Yunfei Xi, Wenhao Pan, Yuanxia Zheng, Yongfa Fan, Jin Cheng, Yu Zhao, Leiwu Zheng
- **연도**: 2022
- **게재지**: Proc. SPIE 12056, Advanced Etch Technology and Process Integration for Nanopatterning XI, 1205607
- **DOI/URL**: https://doi.org/10.1117/12.2613926

## 핵심 요약
DUV litho-etch 케이스에서 딥러닝 기반 etch 모델(ASML-Brion의 Newron etch)을 활용한 full-chip OPC 보정 플로우를 구현하고 검증한다. 대규모 SEM 계측 데이터와 자동화 계측 소프트웨어를 결합하여 복잡한 etch 거동을 캡처하고, 기존 term-based etch 모델 대비 유의미한 정확도 향상을 입증한다.

## 주요 기여
1. **딥러닝 Etch 모델 (Newron etch)**: ASML-Brion의 Newron etch 모델로 복잡한 etch 거동 학습
2. **대규모 계측 데이터 활용**: eP5 e-beam 계측 툴로 대량의 SEM 데이터 수집
3. **자동화 계측 파이프라인**: MXP(ASML-Brion)로 SEM 데이터에서 고품질 gauge 자동 추출
4. **정확도 향상 정량화**: 테스트 패턴 <50%, 실제 칩 패턴 <35% 잔차 오차 감소
5. **Full-chip 적용 검증**: 실제 DUV 리소 공정의 full-chip OPC에 적용

## Recipe/Flow 상세
- **딥러닝 Etch 모델 기반 Full-chip OPC 플로우**:
  1. **대규모 SEM 데이터 수집**:
     - eP5 fast e-beam 계측 툴로 다양한 패턴 SEM 이미지 수집
     - 리소 후(resist) + etch 후 CD 쌍 데이터 확보
  2. **자동 Gauge 추출**:
     - MXP(ASML-Brion) 소프트웨어로 SEM 윤곽 자동 추출
     - 고품질 gauge 필터링 (노이즈 제거, outlier 제외)
  3. **딥러닝 Etch 모델 캘리브레이션**:
     - Newron etch (neural network 기반) 학습
     - 입력: 국소 레이아웃 특징 + resist CD
     - 출력: 최종 etch CD 예측
  4. **Term-based 모델 대비 벤치마크**:
     - 동일 데이터로 term-based etch 모델과 비교
     - 테스트 패턴 및 실제 칩 패턴 모두에서 정확도 평가
  5. **Full-chip OPC 적용**:
     - 딥러닝 etch 모델로 etch 타겟 계산
     - Etch-aware OPC 수렴 → 최종 마스크 생성
- **DUV 공정 특성**: litho-etch 두 단계 모두 고려한 end-to-end 모델
- **평가 지표**: 잔차 오차 감소율 (test: <50%, product: <35%)

## OPC 툴 구현 관련성
- SKOPC의 etch 모델 모듈을 딥러닝 기반으로 업그레이드하는 방법
- 대규모 SEM 데이터 기반 etch 모델 캘리브레이션 파이프라인
- `dl_etch_model.py`: Newron etch 스타일 신경망 etch 모델 구현
- 자동화 gauge 추출 및 품질 필터링 전처리 로직

## 태그
`DeepLearning`, `EtchModel`, `OPC`, `FullChip`, `SEM`, `DUV`, `Calibration`, `Newron`, `SPIE`, `2022`
