# Neural-ILT: Migrating ILT to Neural Networks for Mask Printability and Complexity Co-optimization

## 메타데이터
- **저자**: Bentian Jiang, Lixin Liu, Yuzhe Ma, Hang Zhang, Bei Yu, Evangeline F. Y. Young
- **연도**: 2020
- **게재지/학회**: IEEE/ACM International Conference on Computer-Aided Design (ICCAD 2020), pp. 1-9
- **DOI/URL**: https://dl.acm.org/doi/10.1145/3400302.3415704 / https://github.com/cuhk-eda/neural-ilt
- **인용수**: 150+

## 핵심 요약
Neural-ILT는 역리소그래피 기술(ILT)을 단일 신경망으로 완전히 대체하는 엔드-투-엔드 학습 기반 마스크 최적화기다. 마스크 인쇄 품질(printability), 마스크 복잡도(complexity), 처리 속도(TAT)를 동시에 최적화하는 세 가지 목표를 달성한다. 기존 학습 기반 OPC 및 전통 ILT 플로우 대비 30~70배의 턴어라운드 타임(TAT) 단축을 달성하면서 유사한 마스크 인쇄 품질을 유지하고 마스크 복잡도를 낮춘다.

## 주요 기여
- **엔드-투-엔드 ILT 신경망**: 단일 신경망에서 마스크 예측과 ILT 보정을 동시에 수행
- **3중 목표 공동 최적화**: 마스크 인쇄 품질, 마스크 복잡도, 처리 속도 동시 최적화
- **30~70배 TAT 단축**: 전통 ILT 및 학습 기반 SOTA 대비 대폭 속도 향상
- **오픈소스 구현**: GitHub 공개로 재현성 및 연구 커뮤니티 기여

## Recipe/Process Flow 상세

### Neural-ILT 마스크 최적화 플로우

```
설계 레이아웃 (타겟 패턴)
        ↓
[신경망 기반 초기 마스크 예측]
  - U-Net 계열 인코더-디코더 구조
  - 입력: 타겟 레이아웃 이미지 (이진)
  - 출력: 초기 마스크 예측 (연속값)
        ↓
[ILT 보정 모듈 (학습 가능)]
  - 전통 ILT 반복을 학습 가능한 레이어로 변환
  - 리소그래피 시뮬레이션 통합 (미분 가능)
  - 인쇄 품질 손실 역전파
  - 마스크 복잡도 패널티 (L1 정규화)
        ↓
[공동 최적화 루프]
  - 마스크 예측 + ILT 보정을 단일 순전파로 처리
  - 단일 또는 소수 반복으로 수렴
        ↓
최적화된 마스크 출력
```

### 신경망 아키텍처

**U-Net 기반 마스크 예측기**:
- 인코더: Conv → BN → ReLU (다운샘플링 6단계)
- 디코더: TransposeConv → BN → ReLU (업샘플링 6단계)
- 스킵 커넥션: 인코더-디코더 간 정보 전달

**ILT 보정 레이어**:
- 미분 가능한 리소그래피 이미징 함수 F 내장
- 그래디언트 업데이트: $M_{t+1} = M_t - \alpha \cdot \nabla_{M_t} \mathcal{L}$
- 이 과정을 학습 가능한 파라미터로 변환

### 손실 함수
$$\mathcal{L}_{total} = \mathcal{L}_{print} + \lambda_c \mathcal{L}_{complex}$$

**인쇄 품질 손실**:
$$\mathcal{L}_{print} = \|I(M) - T\|^2 + \text{EPE\_loss}$$

**마스크 복잡도 손실**:
$$\mathcal{L}_{complex} = \|M\|_1 + \text{edge\_penalty}$$
- L1 노름: 마스크 픽셀 수 최소화
- Edge penalty: 마스크 경계 복잡도 (e-beam 샷 수 감소)

### 학습 설정
- 훈련 데이터: ILT 생성 타겟-마스크 쌍
- 배치 크기: 16~32
- 학습률: 1e-3 (Adam 옵티마이저)
- 타일 크기: 256×256 또는 512×512 픽셀

### 성능 비교
| 방법 | TAT | EPE L2 | 마스크 복잡도 |
|------|-----|--------|-------------|
| 전통 ILT | 기준 (수분) | 최소 | 높음 |
| GAN-OPC | ~30배 빠름 | 높음 | 낮음 |
| Neural-ILT | 30~70배 빠름 | 전통 ILT 유사 | 전통 ILT보다 낮음 |

### Neural-ILT 2.0 (TCAD 2022)
확장 버전에서 도메인 특화 최적화 추가:
- 레이어 특화 파인튜닝 (금속/비아/폴리 레이어별)
- 더 나은 복잡도-품질 트레이드오프

## OPC 툴 구현 관련성
Neural-ILT는 SKOPC GNN-OPC의 직접적 비교 대상이자 참조 구현:
- **GNN vs Neural-ILT**: SKOPC의 ResGNN 기반 OPC와 Neural-ILT 직접 성능 비교
- **TAT 목표**: Neural-ILT의 30~70배 가속이 SKOPC TAT 목표 설정의 기준
- **마스크 복잡도 손실**: SKOPC OPC 출력의 마스크 복잡도 제어에 동일 손실 적용
- **오픈소스 참조**: GitHub 코드를 SKOPC 구현 비교 기준으로 활용

## 참고문헌 (핵심)
- Yang et al., "GAN-OPC" (DAC 2018 / TCAD 2020)
- Chen et al., "DAMO" (ICCAD 2020)
- Ronneberger et al., "U-Net" (MICCAI 2015)
- Jiang et al., "Neural-ILT 2.0" (IEEE TCAD 2022)
- LithoBench (NeurIPS 2023)

## 태그
`Neural-ILT`, `ILT`, `End-to-end`, `Mask Optimization`, `OPC`, `U-Net`, `ICCAD 2020`, `Printability`, `Complexity`, `TAT`, `2020`, `Open Source`
