# LithoBench: Benchmarking AI Computational Lithography for Semiconductor Manufacturing

## 메타데이터
- **저자**: Su et al. (CUHK Bei Yu 그룹 + UIUC)
- **연도**: 2023
- **게재지**: NeurIPS 2023 (Datasets and Benchmarks Track), 37th Conference on Neural Information Processing Systems
- **DOI/URL**: https://proceedings.neurips.cc/paper_files/paper/2023/hash/604b9fa9e1c16284e6517d923cf9ff20-Abstract-Datasets_and_Benchmarks.html
- **인용수**: ~40

## 핵심 요약
AI 계산 리소그래피를 위한 포괄적 벤치마크 데이터셋인 LithoBench를 제안한다. 12만 개 이상의 회로 레이아웃 타일로 구성된 대규모 데이터셋으로, 실제 IC 설계에서 크롭한 타일과 유명 ILT 테스트케이스의 레이아웃 토폴로지에 따라 합성된 타일을 포함한다. 리소그래피 시뮬레이션과 마스크 최적화 두 작업에 대해 딥러닝 모델을 설계·평가하는 프레임워크를 제공하며, 최신 모델들을 체계적으로 벤치마킹한다.

## 주요 기여
1. 12만 개 이상 레이아웃 타일의 대규모 계산 리소그래피 벤치마크 데이터셋
2. 리소그래피 시뮬레이션 4개 + 마스크 최적화 4개 모델 설계 및 평가
3. 실제 IC 설계 기반 타일 + ILT 테스트케이스 합성 타일 혼합 구성
4. AI 계산 리소그래피 연구의 표준화된 비교 플랫폼 제공

## Recipe/Process Flow 상세

### 데이터셋 구성
```
LithoBench 데이터셋:
  총 타일 수: >120,000 타일
  타일 크기: 2048×2048 픽셀 (일반적)
  레이어: 단일 레이어 (Metal/Poly)

  데이터 소스:
    실제 IC 설계 크롭:
      - 실제 반도체 회로 레이아웃에서 샘플링
      - 다양한 패턴 밀도 및 복잡도

    합성 타일:
      - ILT 벤치마크 테스트케이스 토폴로지
      - ICCAD 2013 ILT 패턴 기반
      - 제어된 패턴 유형 다양성

Ground Truth 생성:
  리소그래피 시뮬: 물리 기반 Hopkins 공식
  마스크 최적화: ILT 솔버 결과
  레이블: 이진 마스크 + 항공 이미지(aerial image)
```

### 벤치마크 작업 정의
```
작업 1: 리소그래피 시뮬레이션
  입력: 마스크 레이아웃 이미지
  출력: 항공 이미지 (Aerial Image)
  메트릭:
    - MAE (평균 절대 오차)
    - 피어슨 상관계수 (PCC)
    - 시뮬레이션 속도 (ms/타일)

작업 2: 마스크 최적화 (ILT)
  입력: 타겟 레이아웃 (원하는 웨이퍼 패턴)
  출력: 최적화된 마스크 이미지
  메트릭:
    - L2 (마스크 유사도)
    - PVB (공정 변동 밴드)
    - EPE (엣지 배치 오차)
    - 런타임 (초/타일)
```

### 벤치마크 모델
```
리소그래피 시뮬레이션 모델 (4개):
  1. Lithosim (물리 기반 베이스라인)
  2. LithoGAN (GAN 기반)
  3. LithoDiffusion (확산 모델 기반)
  4. CNN 대리 모델 (U-Net 계열)

마스크 최적화 모델 (4개):
  1. ILT 수치 솔버 (베이스라인)
  2. Neural-ILT
  3. GAN-OPC
  4. DevelSet

비교 지표:
  속도: ms~수초/타일 범위
  정확도: EPE nm 범위
  확장성: 전체 칩 적용 가능성
```

### 데이터셋 통계 및 접근
```
공개 저장소: https://github.com/shelljane/lithobench

통계:
  실제 설계 타일: ~80,000+
  합성 타일: ~40,000+
  총: >120,000

데이터 형식:
  입력: PNG 이진 마스크 이미지
  레이블: PNG 항공 이미지
  메타데이터: JSON 파일

활용:
  AI 모델 훈련/검증/테스트 분할
  공정 조건: ArF 193nm (일반적)
  표준 비교: 동일 데이터로 공정한 비교
```

### 성능 결과 (주요 발견)
```
리소그래피 시뮬:
  최고 속도: CNN 대리 ~1ms/타일
  물리 시뮬 대비: ~1000× 가속
  정확도: PCC >0.97 달성 가능

마스크 최적화:
  Neural-ILT: ILT 솔버 대비 ~10× 빠름
  EPE: 수치 ILT 대비 약간 열화

트레이드오프:
  속도 vs. 정확도 명확히 정량화
  → 실용적 방법 선택 기준 제공
```

## OPC 툴 구현 관련성
- **SKOPC 벤치마크**: LithoBench 데이터셋으로 SKOPC 모델 성능 객관적 비교
- **모델 평가**: 리소그래피 시뮬 + 마스크 최적화 메트릭으로 SKOPC 품질 측정
- **데이터 활용**: 12만 타일 데이터를 SKOPC ML 모델 훈련에 활용 가능
- **경쟁 분석**: 벤치마크 모델들과 SKOPC 성능 비교로 개발 우선순위 설정

## 참고문헌
- NeurIPS 2023 Datasets and Benchmarks Track
- GitHub: https://github.com/shelljane/lithobench
- 저자 소속: CUHK (Bei Yu 그룹) + UIUC
- 관련: MaskOpt dataset (arXiv 2025), OpenILT platform (ISEDA 2024)
- 관련: ICCAD 2013 ILT contest 벤치마크

## 태그
`Recipe`, `NeurIPS`, `Benchmark`, `Dataset`, `ComputationalLithography`, `LithographySimulation`, `MaskOptimization`, `ILT`, `AI`, `MachineLearning`, `CUHK`, `BeiYu`, `2023`
