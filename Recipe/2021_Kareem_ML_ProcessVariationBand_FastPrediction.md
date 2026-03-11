# Fast Prediction of Process Variation Band Through Machine Learning Models

## 메타데이터
- **저자**: Pervaiz Kareem, Yonghwi Kwon, Gangmin Cho, Youngsoo Shin
- **연도**: 2021
- **게재지**: Proc. SPIE 11613, Optical Microlithography XXXIV, 1161306
- **DOI/URL**: https://doi.org/10.1117/12.2583805

## 핵심 요약
공정 변동 밴드(PVB: Process Variation Band)의 빠른 계산은 수율 추정, 핫스팟 검출, 마스크 최적화 등 여러 리소그래피 응용에 핵심이다. 기존 리소그래피 시뮬레이션 기반 PVB 계산은 매우 느려 칩의 일부에만 적용 가능하다. 본 논문은 cGAN(조건부 생성적 적대 신경망)을 활용하여 PVB를 고속 고정밀 예측하는 방법을 제안한다.

## 주요 기여
1. **cGAN 기반 PVB 예측**: 조건부 생성적 적대 신경망으로 공정 변동 밴드 직접 예측
2. **500배 속도 향상**: rigorous 리소그래피 시뮬레이션 대비 500× 속도 향상
3. **86% 평균 정확도**: 98% 이상의 패턴에 대해 허용 오차 내 PVB 예측
4. **Full-chip 적용 가능성**: 빠른 예측 속도로 전체 칩 PVB 분석 실현
5. **패턴 커버리지 개선**: 패턴 매칭 방식에서 놓치던 unseen 패턴도 처리

## Recipe/Flow 상세
- **ML 기반 PVB 예측 플로우**:
  1. **데이터 준비**:
     - 다양한 레이아웃 클립 생성 (다양한 패턴 환경 포함)
     - 각 클립에 대해 rigorous 리소그래피 시뮬레이션으로 GT PVB 계산
     - 학습/검증/테스트 데이터셋 분할
  2. **cGAN 모델 학습**:
     - 입력: 레이아웃 클립 이미지 (조건)
     - 생성자 출력: PVB 예측 이미지
     - 판별자: 예측 PVB vs. 실제 PVB 구별
  3. **Full-chip 적용**:
     - 전체 칩을 작은 클립으로 분할
     - 각 클립의 중앙 관심 영역에 대해 PVB 예측
     - 클립 단위 병렬 처리 → full-chip TAT 단축
  4. **PVB 활용**:
     - 핫스팟 검출: PVB가 넓은 영역 → 잠재적 핫스팟
     - OPC 최적화: PVB 최소화 방향으로 OPC 파라미터 조정
     - 수율 추정: 전체 칩 PVB 분포 → 수율 예측
- **PVB 정의**: Focus/dose 변동 범위에서의 패턴 윤곽 변동 영역
- **예측 속도**: 리소 시뮬레이션 대비 500× 빠름
- **정확도**: 98%+ 패턴에서 86% 이상 평균 정확도

## OPC 툴 구현 관련성
- SKOPC의 공정 창 최적화(PWO) 모듈과 연계 가능
- `pvb_predictor.py`: cGAN 기반 빠른 PVB 예측 모듈
- OPC 레시피 최적화 루프에서 빠른 PVB 예측기 활용
- Full-chip 핫스팟 스크리닝에 ML PVB 예측 통합

## 태그
`MachineLearning`, `ProcessVariationBand`, `cGAN`, `OPC`, `Hotspot`, `FullChip`, `Speedup`, `SPIE`, `2021`
