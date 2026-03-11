# SRAF Placement with Generative Adversarial Network

## 메타데이터
- **저자**: Weilun Ciou, Tony Hu, Yi-Yen Tsai, et al.
- **연도**: 2021
- **게재지**: Proc. SPIE 11613, Optical Microlithography XXXIV, 1161305; 확장판: J. Micro/Nanopatterning, Materials, and Metrology 20(4), 041209 (2021)
- **DOI/URL**: https://doi.org/10.1117/12.2581334
- **인용수**: ~25

## 핵심 요약
GAN(Generative Adversarial Network)을 활용하여 SRAF(Sub-Resolution Assist Feature) 배치를 자동화하는 방법론을 제시한다. 기존 Rule-based SRAF와 Model-based SRAF의 속도/정확도 트레이드오프를 GAN이 극복한다. 조건부 GAN(cGAN, pix2pix)을 사용하여 레이아웃 패턴에서 최적 SRAF 배치 마스크를 직접 생성하며, Mentor Graphics(Siemens EDA) TSMC 협력 연구로 양산 공정에서 검증한다.

## 주요 기여
1. GAN 기반 SRAF 직접 생성: 규칙 테이블 없이 레이아웃 → SRAF 마스크 직접 매핑
2. 공정 윈도우 인식 SRAF 배치: 리소그래피 성능 목표 달성
3. Mentor/TSMC 협력 검증: 실제 양산 공정에서 GAN SRAF 검증
4. 기존 Rule-based와 Model-based SRAF 대비 성능 비교 분석

## Recipe/Process Flow 상세

### GAN SRAF의 동기
```
Rule-based SRAF (RB-SRAF):
  방법: Space-Width 테이블에서 SRAF 크기/위치 결정
  장점: 빠름, 단순
  단점: 복잡한 2D 패턴, 밀도 변화 처리 한계

Model-based SRAF (MB-SRAF):
  방법: ILT 또는 리소그래피 시뮬로 최적 SRAF 계산
  장점: 높은 정확도, 공정 윈도우 최대화
  단점: 느림 (수십 시간/전체 칩)

GAN SRAF:
  목표: RB-SRAF 속도 + MB-SRAF 정확도
  훈련: MB-SRAF 결과 학습 → 빠른 추론
  추론: ms 수준 → 전체 칩 수 분
```

### GAN 기반 SRAF 생성 아키텍처
```
모델 유형: 조건부 GAN (pix2pix 기반)

생성기(G):
  입력: 타겟 레이아웃 패턴 이미지 (주 패턴)
  출력: SRAF 배치 이미지 (주 패턴 + SRAF)
  구조: U-Net 인코더-디코더 (skip connections)

판별기(D):
  입력 쌍: (레이아웃, SRAF 배치) → 진짜/가짜
  진짜: MB-SRAF 결과
  가짜: G 생성 SRAF
  구조: PatchGAN (로컬 패치 판별)

손실 함수:
  L_total = L_adversarial + λ_L1 × L_L1 + λ_litho × L_litho
  L_adversarial: GAN 적대적 손실
  L_L1: 픽셀 단위 L1 재구성 손실
  L_litho: 리소그래피 시뮬 기반 공정 윈도우 손실
```

### 훈련 및 추론 흐름
```
훈련 단계:
  1. 다양한 레이아웃 패턴 수집
  2. 각 패턴에 MB-SRAF 적용 → Ground Truth SRAF 배치
  3. (레이아웃, SRAF 배치) 쌍으로 GAN 훈련
  데이터: 수천~수만 클립

추론 단계:
  새 레이아웃 → G(레이아웃) → SRAF 이미지
  SRAF 이미지 → 이진화 → 개별 SRAF 다각형
  MRC 검사 → MRC 위반 SRAF 조정
  → 최종 SRAF 삽입 완료

후처리:
  이미지 → 다각형 변환 (래스터 → 벡터)
  MRC 준수 확인 및 보정
  SRAF 인쇄 마진 검사 (ML-SPC 연동)
```

### 공정 윈도우 인식 손실 함수
```
리소그래피 손실 L_litho:
  GAN 생성 SRAF + 주 패턴 → 시뮬레이션
  다양한 (Focus, Dose) 조건에서 평가:
    PV 밴드: 최소화
    DOF × EL: 최대화
  L_litho = Σ_{(F,D)∈PW} EPE(F,D)²

공정 윈도우 직접 최적화:
  기존 GAN-OPC: 명목 조건만 고려
  GAN SRAF: 공정 변동 조건까지 고려
  → 더 강건한 SRAF 배치
```

### 성능 결과 (Mentor/TSMC 검증)
```
SRAF 배치 품질:
  GAN SRAF vs. MB-SRAF:
    공정 윈도우: 동등하거나 근접
    SRAF 위치 정확도: 높음

  GAN SRAF vs. RB-SRAF:
    공정 윈도우: GAN SRAF 우수
    복잡한 2D 패턴: 특히 개선

런타임:
  MB-SRAF: 수십 시간 (전체 칩)
  GAN SRAF: 수 분 (추론 단계)
  속도 향상: 수백 배

MRC 준수율:
  후처리로 99%+ MRC 준수 달성
```

## OPC 툴 구현 관련성
- **SKOPC GAN SRAF**: `skopc/modeling/sraf_generator.py`에 GAN 기반 SRAF 생성기 추가
- **pix2pix 구현**: PyTorch의 pix2pix 구현 기반으로 SRAF GAN 모델 구축
- **공정 윈도우 손실**: TorchLitho 미분 가능 시뮬레이터로 L_litho 계산
- **Mentor/TSMC 검증**: 양산 공정 실증으로 SKOPC SRAF 신뢰도 기준

## 참고문헌
- Proc. SPIE 11613, Optical Microlithography XXXIV (2021)
- J. Micro/Nanopatterning, Materials, and Metrology 20(4), 041209 (2021)
- 저자 소속: Mentor Graphics (Siemens EDA) + TSMC
- 관련: GAN-based SRAF generation - Alawieh TCAD 2020 (UT Austin)
- 관련: SRAF placement with RL (IEEE ICCAD 2022)
- 관련: SRAF printing prediction using ANN (SPIE 11327, 2020)

## 태그
`Recipe`, `SPIE`, `SRAF`, `GAN`, `GenerativeAdversarialNetwork`, `SRAF-Placement`, `pix2pix`, `ProcessWindow`, `MentorGraphics`, `TSMC`, `2021`
