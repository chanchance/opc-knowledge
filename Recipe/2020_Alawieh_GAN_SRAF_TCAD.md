# GAN-SRAF: Subresolution Assist Feature Generation Using Generative Adversarial Networks

## 메타데이터
- **저자**: Mohamed Baker Alawieh, Yibo Lin, Zaiwei Zhang, Meng Li, Qixing Huang, David Z. Pan
- **연도**: 2020
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD)
- **DOI/URL**: https://doi.org/10.1109/TCAD.2020.2995338 / https://ieeexplore.ieee.org/document/9094711/
- **인용수**: ~150

## 핵심 요약
CGAN(Conditional Generative Adversarial Network)을 이용해 임의의 레이아웃에 대해 직접 SRAF를 생성하는 새로운 SRAF 삽입 프레임워크 GAN-SRAF를 제안한다. 기존 모델 기반 SRAF 삽입은 높은 정확도를 보이지만 계산 비용이 크다는 단점을 극복하며, 런타임을 크게 줄이면서 공정 윈도우 성능을 유지한다.

## 주요 기여
1. CGAN 기반 직접 SRAF 생성 프레임워크 (GAN-SRAF)
2. 임의의 레이아웃 입력에서 즉시 SRAF 맵 생성
3. 모델 기반 SRAF 대비 대폭 단축된 런타임
4. David Z. Pan 그룹 (UT Austin) - OPC/DFM 분야 최고 권위

## Recipe/Process Flow 상세

### CGAN 기반 SRAF 생성 아키텍처
```
입력: 레이아웃 이미지 패치 (binary mask layout)
출력: SRAF 맵 (SRAF 위치/형상을 포함한 이미지)

CGAN 구조:
- 생성기 G: 레이아웃 → SRAF 맵 (U-Net 계열)
  * 인코더: 레이아웃 피처 추출
  * 디코더: SRAF 위치/형상 생성
  * Skip connections: 공간 정보 보존

- 판별기 D: (레이아웃, SRAF 맵) 쌍의 실제/생성 여부 판별
  * 조건부 판별: 입력 레이아웃 조건 고려
  * PatchGAN 구조: 국소 패치 단위 판별

훈련 목적함수:
  L_GAN = E[log D(x,y)] + E[log(1-D(x,G(x)))]
  L_L1  = E[||y - G(x)||₁]   (픽셀 수준 정확도)
  L_total = L_GAN + λ·L_L1
```

### GAN-SRAF 추론 파이프라인
```
1. 레이아웃 전처리
   - 전체 칩 레이아웃을 고정 크기 패치로 분할
   - 각 패치: 주 패턴 바이너리 이미지

2. CGAN 추론 (각 패치)
   - 학습된 G(x) 적용
   - 출력: SRAF 후보 맵 (연속값 또는 이진값)

3. 후처리
   - SRAF 후보 맵 이진화 (임계값 적용)
   - DRC/MRC 규칙 체크 및 조정
   - 인접 패치 경계 처리 (패치 병합)

4. 전체 칩 SRAF 맵 조합
   - 패치별 결과 스티칭
   - 패치 경계 충돌 해결
```

### 성능 결과
```
런타임: 모델 기반 SRAF 대비 대폭 단축
EPE: 동등 또는 근접
PV Band: 유사한 공정 윈도우 확장
SRAF 품질: Calibre model-based SRAF와 시각적/정량적 유사성
```

### 훈련 데이터
- Ground Truth: Calibre 기반 model-based SRAF 결과
- 다양한 레이아웃 패턴 (1D, 2D, contact/via)
- 데이터 증강: 회전, 반전

## OPC 툴 구현 관련성
- **SKOPC SRAF 생성기**: `skopc/modeling/sraf_generator.py`에 CGAN 기반 추론 통합 가능
- **빠른 추론**: GPU 기반 CGAN 추론으로 전체 칩 SRAF 생성 시간 단축
- **발전 계보**: Supervised DL(2018) → GAN-SRAF(2020) → CTM-SRAF(2023)의 SRAF ML 발전 계보
- **David Z. Pan / Yibo Lin**: UT Austin → PKU 그룹, SKOPC의 GNN-OPC와 동일 분야 최고 그룹

## 참고문헌
- IEEE TCAD 2020, DOI: 10.1109/TCAD.2020.2995338
- 저자 소속: UT Austin (Pan), UT Austin (Alawieh, Lin)
- 관련: CTM-SRAF (IEEE TCAD, 2023)
- 관련: Subresolution Assist Feature Generation With Supervised Data Learning (IEEE TCAD, 2018)
- 관련: 2025_Li_CurvilinearSRAF (이미 수집됨)

## 태그
`Recipe`, `IEEE`, `TCAD`, `SRAF`, `GAN`, `CGAN`, `GenerativeAdversarialNetwork`, `DeepLearning`, `Runtime`, `ProcessWindow`, `DavidZPan`, `YiboLin`
