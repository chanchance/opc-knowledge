# Novel Methodology for SRAF Placement over a Machine Learning Generated Probability Map

## 메타데이터
- **저자**: Yi-Ting Lin, Sean Shang-En Tseng, Iris Hui-Ru Jiang, James P. Shiely
- **소속**: (SPIE DTCO and Computational Patterning 2022 게재)
- **연도**: 2022
- **게재지**: Proc. SPIE 12052, DTCO and Computational Patterning, 120520X
- **DOI/URL**: https://doi.org/10.1117/12.2613681

## 핵심 요약
머신러닝으로 생성된 SRAF 배치 확률 맵(probability map) 위에 SRAF를 배치하는 새로운 방법론을 제안한다. ML 모델이 레이아웃 각 위치에서 SRAF 배치의 유익성(benefit)을 확률값으로 예측하고, 이 확률 맵을 기반으로 MRC를 준수하는 실제 SRAF 형상을 결정한다. 기존 ILT 기반 SRAF 삽입 대비 훨씬 빠른 속도로 고품질 SRAF 배치를 달성한다.

## 주요 기여
1. **ML 확률 맵 기반 SRAF 배치**: ML 모델이 각 픽셀/위치에서 SRAF 유익성 확률 예측 → 빠른 SRAF 후보 영역 결정
2. **확률 맵 → 실제 SRAF 변환**: 확률 맵에서 MRC를 준수하는 실제 SRAF 형상 도출 알고리즘
3. **ILT 대비 속도 향상**: ML inference 기반으로 ILT의 계산 부담 없이 유사한 품질의 SRAF 삽입
4. **Data-driven 접근**: 레이아웃 특성만으로 SRAF 필요 위치 예측 — 물리 모델 없이 적용 가능
5. **Full-chip 확장성**: 확률 맵 생성의 빠른 속도로 전체 칩 규모 적용 가능

## Recipe/Flow 상세
```
[ML Probability Map SRAF Flow]
1. ML 모델 훈련 (오프라인):
   - 입력: 레이아웃 패턴 이미지/특성
   - 레이블: ILT 기반 SRAF usefulness map (ground truth)
   - 모델: CNN 또는 U-Net 계열 (픽셀별 확률 예측)
2. SRAF 확률 맵 생성 (온라인):
   - 입력 레이아웃 → 훈련된 ML 모델 추론
   - 출력: 각 위치의 SRAF 배치 확률 맵 (0~1)
3. 확률 맵 → SRAF 형상 변환:
   - 확률 임계값(threshold) 이상 영역 추출
   - MRC(최소 선폭, 최소 간격) 적용하여 valid SRAF 형상 생성
   - SRAF 인쇄 위험 영역 마스킹
4. OPC와 통합:
   - 생성된 SRAF를 main feature OPC와 함께 처리
   - 최종 검증: SRAF printing check + process window 평가
```

### 핵심 파라미터
- **ML 모델 유형**: CNN/U-Net 계열 (픽셀별 확률 출력)
- **훈련 레이블**: ILT 기반 SRAF usefulness map
- **확률 임계값**: MRC 및 SRAF printing 위험 기반 조정
- **속도**: ILT 대비 대폭 향상 (ML inference 시간만 소요)

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: SRAF 삽입 단계에 ML 확률 맵 방식 통합 참고
- `skopc/modeling/gnn/`: GNN 기반 SRAF 확률 맵 생성기 구현 시 이 논문 방법론 참고
- **Data-driven SRAF**: SKOPC의 SRAF 삽입 모듈을 ML 기반으로 고도화하는 핵심 참고 문헌
- `recipes/example_euv.yaml`: EUV 노드 SRAF 삽입 방법(`sraf_method: ml_probability_map`) 파라미터 설계 참고

## 태그
`Recipe`, `SPIE`, `SRAF`, `Machine Learning`, `Probability Map`, `CNN`, `U-Net`, `DTCO`, `Full-Chip`, `2022`
