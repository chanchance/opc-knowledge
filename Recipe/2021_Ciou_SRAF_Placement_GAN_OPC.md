# SRAF Placement with Generative Adversarial Network

## 메타데이터
- **저자**: Weilun Ciou, Tony Hu, Y. Y. Tsai, Terry Hsuan, Elvis Yang, T. H. Yang, K. C. Chen
- **연도**: 2021
- **게재지**: Proc. SPIE 11613, Optical Microlithography XXXIV, 1161305
- **DOI/URL**: https://doi.org/10.1117/12.2581334

## 핵심 요약
SRAF(Sub-Resolution Assist Feature) 삽입에 GAN(Generative Adversarial Network)을 적용하여, 기존 모델 기반 SRAF 대비 144배 빠른 full-chip SRAF 배치를 실현한다. 이전 ML 기반 SRAF 방법 대비 약 14배 속도 향상을 달성하면서도 동등한 리소그래피 품질을 유지한다.

## 주요 기여
1. **GAN 기반 SRAF 배치**: 생성적 적대 신경망으로 SRAF 위치와 크기를 직접 예측
2. **144배 속도 향상**: 기존 모델 기반 SRAF 대비 런타임 144배 단축
3. **14배 ML 속도 향상**: 이전 DCNN 기반 ML SRAF 방법 대비 14배 빠름
4. **동등한 리소그래피 품질**: 속도 향상에도 공정 창, NILS 등 리소 지표 동등 수준 유지
5. **Full-chip 적용 가능성**: 빠른 예측 속도로 전체 칩 SRAF 삽입 실용화

## Recipe/Flow 상세
- **GAN 기반 SRAF 배치 플로우**:
  1. **학습 데이터 준비**:
     - 레이아웃 클립 이미지 (조건 입력)
     - 기존 모델 기반 SRAF 결과 또는 CTM(Continuous Transmission Mask) 이미지 (Ground Truth)
     - 다양한 패턴 환경(밀도, 방향, 피치 등) 포함
  2. **조건부 GAN 학습**:
     - 생성자(Generator): 레이아웃 → SRAF 배치 이미지 생성
     - 판별자(Discriminator): 생성된 SRAF vs. 실제 SRAF 구별
     - 조건 입력: 레이아웃 패턴 이미지
  3. **SRAF 이미지 → 폴리곤 변환**:
     - GAN 출력 이미지에서 SRAF 윤곽 추출
     - 마스크 룰 체크(MRC) 준수하는 SRAF 폴리곤 생성
  4. **OPC와의 통합**:
     - GAN-SRAF 배치 결과 → OPC 모델 입력
     - SRAF 포함 레이아웃에 대해 주 패턴 OPC 수행
  5. **품질 검증**:
     - NILS, 공정 창, CD 균일도 측정
     - 모델 기반 SRAF 결과와 비교
- **GAN 장점**: 병렬 추론으로 클립 단위 초고속 SRAF 예측, 패턴 매칭 방식의 한계 극복
- **적용 노드**: 선진 ArF/EUV 리소그래피 SRAF 삽입

## OPC 툴 구현 관련성
- SKOPC SRAF 삽입 모듈에서 GAN 기반 고속 SRAF 배치 구현
- `gan_sraf.py`: cGAN 모델 학습 및 추론, SRAF 이미지→폴리곤 변환
- 기존 모델 기반 SRAF를 ML 예측으로 대체하여 런타임 단축
- SRAF+OPC 통합 플로우에서 GAN 예측 → OPC fine-tuning 하이브리드

## 태그
`SRAF`, `GAN`, `MachineLearning`, `OPC`, `FullChip`, `Speedup`, `AssistFeature`, `SPIE`, `2021`
