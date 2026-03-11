# LithoHoD: A Litho Simulator-Powered Framework for IC Layout Hotspot Detection

## 메타데이터
- **저자**: Hao-Chiang Shao, Guan-Yu Chen, Yu-Hsien Lin, Chia-Wen Lin, Shao-Yun Fang, Pin-Yian Tsai, Yan-Hsiu Liu
- **연도**: 2024
- **게재지/학회**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD)
- **DOI/URL**: https://arxiv.org/abs/2409.10021
- **인용수**: 미확인 (신규 논문)

## 핵심 요약
LithoHoD는 리소그래피 시뮬레이터와 객체 검출 백본을 통합하여 IC 레이아웃 핫스팟 검출 성능을 향상시키는 프레임워크다. 형상 특징 추출기(RetinaNet)와 리소그래피 시뮬레이터(LithoNet)를 결합하고, 크로스-어텐션 블록으로 형상 특징과 리소그래피 변형 특징을 융합한다. 시뮬레이션된 ICCAD16과 실세계 데이터셋 모두에서 기존 최고 성능 방법들을 능가하며, 특히 실세계 데이터셋에서의 일반화 성능이 우수하다.

## 주요 기여
- **듀얼 검출 접근법**: 물리적 리소그래피 변형 위험과 학습된 문제 패턴을 동시에 검출
- **크로스-어텐션 통합**: 리소그래피 시뮬레이터의 피처와 객체 검출기의 피처를 크로스-어텐션으로 융합
- **실세계 데이터 일반화**: 시뮬레이션 데이터로 학습하면서 실세계 데이터셋에서 강건한 성능 달성
- **피처 피라미드 네트워크**: 다중 스케일 핫스팟 패턴 검출을 위한 FPN 구조 채택
- **리소그래피 물리 통합**: 순수 데이터 기반 접근법의 한계를 리소그래피 물리 시뮬레이션으로 보완

## 검증 방법론
- **ICCAD 2016 벤치마크**: 표준 시뮬레이션 기반 핫스팟 검출 벤치마크로 성능 평가
- **실세계 데이터셋 검증**: 실제 IC 레이아웃에서 취득한 핫스팟 데이터로 일반화 성능 평가
- **비교 기준선**: 이전 최고 성능(SOTA) 방법들과 동일한 데이터 분할로 직접 비교
- **크로스 도메인 평가**: 시뮬레이션 도메인 → 실세계 도메인 전이 성능 측정
- **어텐션 절제 연구**: 크로스-어텐션 모듈 기여도를 절제 실험으로 정량화

## 검증 지표
- **EPE 허용 범위**: 리소그래피 시뮬레이터 기반 변형량으로 핫스팟 정의
- **사용 시뮬레이터**: LithoNet (학습 가능한 리소그래피 시뮬레이터), ICCAD 2016 벤치마크 시뮬레이션
- **검증 커버리지**: ICCAD16 벤치마크 + 실세계 데이터셋 (두 가지 독립 평가)
- **주요 메트릭**: Recall, AUC (Area Under Curve), 핫스팟 검출률, 오탐률(False Positive Rate)
- **계산 복잡도**: 기존 방법 대비 약간 높은 연산 시간 (정확도-속도 트레이드오프)

## OPC 툴 구현 관련성
SKOPC의 OPC 후처리 검증 및 핫스팟 분석 모듈에 다음과 같이 활용 가능:
1. **물리 기반 핫스팟 검출**: 리소그래피 시뮬레이터를 핫스팟 검출에 통합하는 LithoHoD 아키텍처 도입
2. **OPC 검증 후처리**: OPC 적용 후 레이아웃에서 잔존 핫스팟을 자동으로 검출
3. **크로스-어텐션 피처 융합**: 레이아웃 패턴 특징과 리소그래피 시뮬레이션 결과를 통합하는 검증 엔진
4. **실세계 적용성**: 학습 데이터와 다른 실제 공정에도 적용 가능한 범용 핫스팟 검출기
5. **EPE 기반 핫스팟 정의**: LithoNet의 변형 예측을 EPE 계산에 활용하는 방법론

## 참고문헌 (핵심)
- ICCAD 2016 핫스팟 검출 벤치마크 데이터셋
- Lin et al. (2021) - Federated Learning 기반 핫스팟 검출
- RetinaNet (Lin et al., 2017) - 객체 검출 백본
- LithoNet - 학습 가능한 리소그래피 시뮬레이터
- Unitho (Jin et al., 2025) - 통합 컴퓨테이셔널 리소그래피 프레임워크

## 태그
`Verification`, `OPC`, `Hotspot Detection`, `Lithography Simulation`, `Deep Learning`, `Cross-Attention`, `RetinaNet`, `TCAD`, `ICCAD`, `2024`, `Real-world Dataset`, `Pattern Fidelity`
