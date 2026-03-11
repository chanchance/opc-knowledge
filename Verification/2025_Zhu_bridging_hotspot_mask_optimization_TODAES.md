# Bridging Hotspot Detection and Mask Optimization via Domain-Crossing Masked Layout Modeling

## 메타데이터
- **저자**: Binwu Zhu, Su Zheng, Yuzhe Ma, Bei Yu, Martin D.F. Wong (CUHK)
- **연도**: 2025
- **게재지/학회**: ACM Transactions on Design Automation of Electronic Systems (TODAES), Vol. 30, No. 4, pp. 54:1–54:20
- **DOI/URL**: https://dl.acm.org/doi/10.1145/3728468
- **인용수**: 미확인 (2025년 최신 논문)

## 핵심 요약
OPC(광학 근접 보정)와 핫스팟 검출(HSD)을 통합한 단일 딥러닝 모델을 제안한다. 두 태스크를 통합하면 각각의 성능이 향상된다는 핵심 아이디어를 바탕으로, 마스크 모델링(masked modeling) 기법으로 레이아웃 이해 모델을 사전 학습하여 레이아웃 기하 정보를 효과적으로 포착한다. 사전 학습된 모델은 제한된 데이터로 HSD와 OPC 모두에 쉽게 미세 조정될 수 있다. 도메인 교차(domain-crossing) 방식으로 HSD와 OPC의 상호 보완적 정보를 공유하여 두 태스크 모두의 성능을 향상시킨다.

## 주요 기여
- **OPC-HSD 통합 프레임워크**: 마스크 최적화와 핫스팟 검출을 단일 모델에서 통합
- **마스크 레이아웃 모델링 사전 학습**: 마스크 모델링 기법으로 레이아웃 기하 정보 사전 학습
- **도메인 교차 전이 학습**: OPC와 HSD 간 도메인을 교차하는 지식 전이
- **제한 데이터 미세 조정**: 소량의 레이블 데이터로 두 태스크 모두 효과적 미세 조정
- **상호 태스크 성능 향상**: 통합으로 HSD와 OPC 각각의 성능이 모두 향상됨

## 검증 방법론
- **HSD 태스크 평가**: ICCAD 벤치마크에서 핫스팟 검출 정확도 측정
- **OPC 태스크 평가**: EPE 및 PVB 기준 마스크 최적화 품질 측정
- **통합 효과 측정**: 단독 HSD/OPC 모델 대비 통합 모델의 성능 향상 정량화
- **도메인 교차 효과 절제 연구**: 도메인 교차 전이의 기여도 분리 측정
- **소량 데이터 실험**: 다양한 레이블 데이터 양에서의 성능 비교

## 검증 지표
- **HSD 정확도**: 핫스팟 분류 정확도, 미스율, 오탐률
- **OPC EPE**: EPE 위반 수 및 최대 EPE
- **PVB**: 공정 변동 견고성
- **사용 시뮬레이터**: ICCAD 벤치마크 리소그래피 시뮬레이터
- **검증 커버리지**: ICCAD 벤치마크 HSD + OPC 데이터셋

## OPC 툴 구현 관련성
SKOPC의 OPC 및 검증 통합 파이프라인에 다음과 같이 활용 가능:
1. **OPC-검증 통합 모델**: SKOPC에서 OPC 최적화와 핫스팟 검출을 단일 모델로 통합
2. **사전 학습 레이아웃 모델**: 마스크 모델링으로 사전 학습된 레이아웃 표현 모델을 SKOPC에 활용
3. **도메인 교차 지식 전이**: OPC에서 얻은 레이아웃 이해를 검증에, 검증 피드백을 OPC에 활용
4. **데이터 효율적 캘리브레이션**: 사전 학습 모델의 소량 데이터 미세 조정으로 새 공정 노드 빠르게 적응
5. **통합 검증 워크플로우**: OPC → 핫스팟 검출 → OPC 재조정의 통합 루프 구현

## 참고문헌 (핵심)
- Yang et al. (2020) - GAN-OPC (OPC 태스크 기준선)
- Geng et al. (2022) - Attention-based hotspot detection (HSD 태스크 기준선)
- BERT (Devlin et al., 2019) - 마스크 언어 모델 원형
- MAE (He et al., 2022) - 마스크 오토인코더 원형
- ICCAD 벤치마크 데이터셋

## 태그
`Verification`, `OPC`, `Hotspot Detection`, `Unified Framework`, `Masked Layout Modeling`, `Domain Crossing`, `Transfer Learning`, `TODAES`, `2025`, `CUHK`, `Pre-training`, `Fine-tuning`, `EPE`, `PVB`
