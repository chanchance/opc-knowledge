# A Physics-Constrained, Design-Driven Methodology for Defect Dataset Generation in Optical Lithography

## 메타데이터
- **저자**: Yuehua Hu, Jiyeong Kong, Dong-yeol Shin, Jaekyun Kim, Kyung-Tae Kang
- **연도**: 2025
- **게재지/학회**: arXiv:2512.09001 (cs.CV)
- **DOI/URL**: https://arxiv.org/abs/2512.09001
- **인용수**: 신규 논문 (2025년 12월)

## 핵심 요약
반도체 리소그래피 결함 검사용 AI 학습 데이터 부족 문제를 해결하는 물리 제약 방법론을 제안한 논문. 수학적 형태학 연산(침식·팽창)으로 물리적으로 타당한 결함 레이아웃을 합성하고, DMD(Digital Micromirror Device) 기반 리소그래피로 실제 제작하여 픽셀 수준 레이블이 달린 3,530장의 광학 현미경 이미지와 13,365개의 결함 인스턴스 데이터셋을 구축한다.

## 주요 기여
- 물리 제약 수학적 형태학 연산(침식·팽창)으로 현실적 결함 레이아웃 합성
- DMD 리소그래피로 합성 결함 패턴을 실제 물리 샘플로 제작
- 결함/무결함 광학 현미경 비교로 픽셀 수준 정밀 레이블 생성
- 4가지 결함 클래스: bridge, burr, pinch, contamination
- Mask R-CNN vs Faster R-CNN 비교: Mask R-CNN이 약 34-42% AP@0.5 향상

## 알고리즘/수식
- **수학적 형태학 결함 생성**:
  - 침식(Erosion): A⊖B = {x | B_x ⊆ A}  → 패턴 수축 → "pinch" 결함 모사
  - 팽창(Dilation): A⊕B = {x | B_x ∩ A ≠ ∅}  → 패턴 확장 → "bridge" 결함 모사
  - 구조 요소 B: 결함 형태와 크기 제어

- **물리 제약 조건**:
  - 침식량 제한: 패턴이 완전히 사라지지 않도록 최소 폭 보장
  - 팽창량 제한: 인접 패턴과 합쳐지지 않도록 최소 공간 보장
  - 실제 공정에서 발생 가능한 결함 범위 내로 파라미터 제한

- **DMD 리소그래피 제작**:
  - 합성 결함 레이아웃 → DMD 패턴 → 광학 리소그래피 노광
  - 결함 있는 패턴 vs 결함 없는 패턴 쌍(pair) 제작

- **픽셀 수준 레이블 생성**:
  - 결함 이미지 I_defect와 무결함 이미지 I_clean 비교
  - |I_defect - I_clean| > threshold → 결함 마스크

- **성능 결과**:
  | 결함 유형 | Mask R-CNN AP@0.5 | Faster R-CNN AP@0.5 |
  |----------|-------------------|---------------------|
  | Bridge   | 0.980             | 0.740               |
  | Burr     | 0.965             | 0.719               |
  | Pinch    | 0.971             | 0.717               |

## OPC 툴 구현 관련성
SKOPC의 DRC 및 리소그래피 결함 검사 기능 확장에 활용 가능. 현재 SKOPC의 `skopc/layout/drc.py`가 기하학적 규칙 위반을 체크하지만, 리소그래피 공정 결함(bridge, pinch 등)은 다른 접근이 필요. 물리 제약 형태학 연산으로 SKOPC 테스트 데이터의 결함 패턴 자동 생성 가능. LithoEngine 출력에서 이런 결함 예측 모듈 추가 시 참조.

## 참고문헌 (핵심)
- He et al., "Mask R-CNN," ICCV (2017) — 인스턴스 세분화 모델
- Serra, "Image Analysis and Mathematical Morphology" — 형태학 이론
- DMD 리소그래피 관련 광학 장비 논문들

## 태그
`defect-detection`, `optical-lithography`, `morphology`, `erosion-dilation`, `dataset-generation`, `Mask-RCNN`, `physics-constrained`, `DMD`, `2025`, `arxiv`
