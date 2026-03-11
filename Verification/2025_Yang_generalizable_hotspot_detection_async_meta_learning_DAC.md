# Generalizable Lithographic Hotspot Detection Using Asynchronous Meta-Learning with Only One Shot

## 메타데이터
- **저자**: Haoyu Yang, Jing Su, Yi Zou, Yuzhe Ma, Bei Yu, Evangeline F.Y. Young
- **연도**: 2025
- **게재지**: Proceedings of the 62nd Annual ACM/IEEE Design Automation Conference (DAC 2025)
- **DOI/URL**: https://doi.org/10.1109/DAC63849.2025.11132646

## 핵심 요약
기존 CNN 기반 핫스팟 탐지기가 훈련된 설계 이외의 회로 레이아웃에 일반화되지 않는 문제를 해결하는 퓨샷(few-shot) 학습 기반 프레임워크를 제시한다. 비동기 메타-러닝(asynchronous meta-learning) 방식을 개발하여 CNN 특징 추출과 분류 컴포넌트를 비동기적으로 업데이트함으로써 단 1개의 훈련 레이아웃 클립만으로 새로운 설계에 빠르게 적응 가능한 메타-초기화 모델을 획득한다. ICCAD 2012, 2019 데이터셋에서 기존 방법보다 우수한 일반화 성능을 실증한다.

## 주요 기여
1. **비동기 메타-러닝(Asynchronous Meta-Learning)**: CNN 특징 추출기와 분류기를 비동기적으로 업데이트하는 새로운 메타-러닝 방식
2. **원샷(One-Shot) 적응**: 단 1개의 훈련 클립으로 새로운 설계 레이아웃에 적응
3. **레이아웃 토폴로지 기반 샘플링 전략**: 퓨샷 적응의 일반화 안정성 향상
4. 미지 새 설계에 대한 우수한 일반화 성능 달성 (ICCAD 2012, 2019 벤치마크)
5. 다양한 회로 레이아웃 간 핫스팟 탐지 이식성(portability) 실현

## 검증 방법론
- **벤치마크 데이터셋**: ICCAD 2012, ICCAD 2019 핫스팟 탐지 데이터셋
- **평가 설정**: Cross-design 일반화 - 훈련 설계와 다른 미지 새 설계에서 평가
- **훈련 데이터**: 원샷(one-shot) - 새 설계에서 레이아웃 클립 1개만 사용
- **비교 기준**: 기존 CNN 기반 핫스팟 탐지기들 (prior arts)
- **평가 지표**: 새 설계에 대한 일반화 성능 (정확도, 일반화 안정성)
- **결론**: 비동기 메타-러닝이 기존 방법 대비 미지 설계 일반화에서 우수

## OPC 툴 구현 관련성
- 고객별 다양한 레이아웃에 일반화 가능한 핫스팟 탐지 모델 구축 전략
- 새 공정/설계에 빠르게 적응하는 OPC 검증 AI 모델의 퓨샷 전이학습 방법론
- 메타-러닝 기반 핫스팟 탐지를 OPC post-verification 단계에 통합하는 참조
- 소량 라벨 데이터로 새 레이아웃/공정에 적응하는 practical OPC 검증 솔루션

## 태그
`Verification`, `Hotspot`, `MetaLearning`, `FewShot`, `Generalization`, `CNN`, `DeepLearning`, `DAC`, `IEEE`, `2025`
