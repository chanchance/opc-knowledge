# Bridging Hotspot Detection and Mask Optimization via Domain-Crossing Masked Layout Modeling

## 메타데이터
- **저자**: Binwu Zhu, Su Zheng, Yuzhe Ma, Bei Yu, Martin D. F. Wong
- **연도**: 2025
- **게재지**: ACM Transactions on Design Automation of Electronic Systems (TODAES), Vol. 30, No. 4, pp. 54:1–54:20
- **DOI/URL**: https://doi.org/10.1145/3728468
- **인용수**: ~5

## 핵심 요약
OPC(Optical Proximity Correction)와 핫스팟 탐지(HSD: Hotspot Detection)를 통합 딥러닝 모델로 연결하는 도메인 교차(domain-crossing) 마스크 레이아웃 모델링 프레임워크를 제안한다. 마스크 모델링 기법으로 구축된 레이아웃 이해 모델을 사전 훈련하여 레이아웃 기하 정보를 효과적으로 포착하고, 이를 HSD와 OPC 두 태스크에 미세 조정(fine-tuning)함으로써 제한된 데이터로도 두 태스크 모두 성능을 향상시킨다.

## 주요 기여
1. OPC와 핫스팟 탐지를 통합 사전 훈련 모델로 연결
2. 마스크 레이아웃 모델링 기법으로 레이아웃 기하 정보 표현 학습
3. 도메인 교차 전이 학습: HSD → OPC, OPC → HSD 지식 전달
4. 제한된 레이블 데이터로 두 태스크 모두 개선 (데이터 효율성)

## Recipe/Process Flow 상세

### OPC와 HSD의 관계
```
핫스팟 탐지 (HSD):
  목적: 레이아웃에서 리소그래피 실패 위험 패턴 검출
  입력: 설계 레이아웃 또는 post-OPC 레이아웃
  출력: 핫스팟/비핫스팟 분류
  한계: OPC 없이 핫스팟 → OPC 후 해결될 수도 있음

OPC:
  목적: 마스크 패턴 수정으로 웨이퍼 CD 정확도 향상
  입력: 설계 레이아웃 → 출력: 최적화 마스크
  한계: OPC 최적화 결과가 핫스팟 여부 영향

OPC-HSD 상호의존성:
  OPC 품질 → 핫스팟 발생 여부에 직접 영향
  핫스팟 위치 지식 → OPC 최적화 방향 안내
  통합 학습: 두 태스크 공통 레이아웃 특징 공유
```

### 도메인 교차 마스크 레이아웃 모델링
```
마스크 레이아웃 언어 모델:
  레이아웃 → 패치(patch) 시퀀스 변환
  트랜스포머(Transformer) 아키텍처
  마스크 모델링(Masked Modeling):
    입력 패치 일부 마스킹 → 마스크된 패치 예측
    BERT 스타일 자기 지도 학습

사전 훈련 (Pre-training):
  레이블 없는 대규모 레이아웃 데이터
  마스크 패치 예측 태스크 → 레이아웃 기하 이해 학습
  출력: 레이아웃 기하 특징 표현 (embeddings)

도메인 교차 미세 조정:
  HSD 태스크:
    사전 훈련 인코더 → HSD 분류 헤드
    레이블: 핫스팟/비핫스팟
  OPC 태스크:
    사전 훈련 인코더 → OPC 마스크 생성 헤드
    레이블: Ground Truth 마스크 (ILT 결과)
  교차 학습:
    HSD 학습 → OPC 개선 (핫스팟 지식 활용)
    OPC 학습 → HSD 개선 (마스크 변형 이해)
```

### 전이 학습 효과
```
데이터 효율성:
  사전 훈련 없이: 많은 레이블 데이터 필요
  사전 훈련 후 미세 조정: 소량 레이블 데이터로 고성능

도메인 교차 이점:
  HSD → OPC 전이:
    핫스팟 패턴 지식 → OPC가 핫스팟 유발 패턴 우선 교정
  OPC → HSD 전이:
    마스크 변형 이해 → OPC 후 핫스팟 예측 정확도 향상

공통 특징:
  두 태스크 모두: 리소그래피 근접 효과 이해 필요
  사전 훈련 인코더: 공통 레이아웃 물리 특징 학습
```

### 성능 결과
```
HSD 성능:
  도메인 교차 모델: 단독 HSD 모델 대비 개선
  소량 데이터: 사전 훈련으로 적은 레이블 데이터로 동등 성능

OPC 성능:
  도메인 교차 모델: 단독 OPC 모델 대비 개선
  EPE 감소: HSD 지식 통합으로 핫스팟 위치 OPC 강화

통합 효율성:
  단일 모델로 HSD + OPC 동시 처리
  OPC-검증-재OPC 루프 단축
```

## OPC 툴 구현 관련성
- **SKOPC HSD-OPC 통합**: 핫스팟 탐지 결과를 OPC 최적화에 피드백
- **사전 훈련 레이아웃 모델**: 대규모 레이아웃에서 사전 훈련 후 SKOPC OPC 미세 조정
- **핫스팟 우선 OPC**: HSD 결과로 핫스팟 위치 OPC 집중 최적화
- **데이터 효율**: 소량 레이블 데이터로 신규 노드 OPC/HSD 빠른 적응

## 참고문헌
- ACM TODAES, Vol. 30, No. 4, pp. 54:1–54:20 (2025)
- 저자 소속: CUHK (Bei Yu, Martin Wong 그룹)
- 관련: RuleLearner (TCAD 2025)
- 관련: L2O-ILT (TCAD 2024)
- 관련: ML hotspot detection (SPIE 10451, 2017)

## 태그
`Recipe`, `TODAES`, `ACM`, `HotspotDetection`, `OPC`, `MaskOptimization`, `TransferLearning`, `MaskedModeling`, `Transformer`, `DomainCrossing`, `CUHK`, `BeiYu`, `2025`
