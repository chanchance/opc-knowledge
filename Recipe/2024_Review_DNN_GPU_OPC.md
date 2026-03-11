# A Review of DNN and GPU in Optical Proximity Correction

## 메타데이터
- **저자**: (IEEE 문서 10617556, 저자 정보 상세 접근 필요)
- **소속**: 미상 (IEEE 게재)
- **연도**: 2024
- **게재지**: IEEE Conference Publication
- **DOI/URL**: https://ieeexplore.ieee.org/document/10617556/

## 핵심 요약
딥 뉴럴 네트워크(DNN)와 GPU를 OPC에 활용하는 연구 동향을 종합 리뷰한다. OPC 문제 해결을 위해 우수한 알고리즘, 충분한 컴퓨팅 파워, 적절한 데이터셋이 필요함을 명확히 하고, CNN·GNN·GAN·Transformer 등 다양한 딥러닝 알고리즘이 OPC 정확도를 개선한 핵심 연구들을 정리하며 미래 방향을 전망한다.

## 주요 기여
1. **체계적 리뷰**: CNN, GNN, GAN, Transformer 기반 OPC 연구의 체계적 분류 및 비교
2. **GPU 가속 OPC**: GPU를 통한 OPC 계산 속도 향상 연구 흐름 정리
3. **알고리즘-데이터-컴퓨팅 삼각 프레임워크**: OPC에서 DNN 성공의 세 가지 필수 요소 명확화
4. **미래 방향 제시**: DNN/GPU 기반 OPC의 미개척 과제 및 연구 방향 전망
5. **실용적 가이드**: 연구자/엔지니어를 위한 DNN OPC 방법론 선택 가이드

## Recipe/Flow 상세 (리뷰 논문 기반 분류 체계)

### DNN OPC 알고리즘 분류
```
1. CNN 기반 OPC:
   - 리소그래피 시뮬레이션 가속 (forward model)
   - 마스크 최적화 예측 (inverse OPC)
   - 예: LithoNet, OPCNet, DAMO

2. GNN 기반 OPC:
   - Edge segment graph 기반 EPE 예측
   - 패턴 간 공간 관계 학습
   - 예: GNN-OPC (Sun et al.)

3. GAN 기반 OPC:
   - Mask 생성 (generator) + 리소 검증 (discriminator)
   - 예: GAN-OPC, GAN-SRAF

4. Transformer 기반 OPC:
   - 장거리 패턴 의존성 학습
   - Attention 메커니즘으로 복잡한 근접 효과 모델링

5. GPU 가속 OPC:
   - 리소그래피 시뮬레이션 병렬화
   - 예: cuLitho (NVIDIA)
```

### 핵심 파라미터
- **알고리즘 분류**: CNN / GNN / GAN / Transformer
- **가속 수단**: GPU 병렬 컴퓨팅
- **성능 지표**: OPC 정확도(EPE), 속도(runtime), 데이터 효율성
- **리뷰 범위**: 2018~2024년 주요 DNN OPC 연구

## OPC 툴 구현 관련성
- `skopc/modeling/gnn/`: GNN-OPC 구현의 이론적 배경 및 관련 연구 전체 흐름 파악에 활용
- **알고리즘 선택**: SKOPC의 ML 기반 OPC 모듈 확장 시 CNN/GNN/GAN/Transformer 중 선택 근거 제공
- **GPU 가속**: SKOPC의 리소그래피 시뮬레이션 GPU 가속(TorchLitho) 도입 배경 이해
- `skopc/modeling/`: 새로운 DNN 기반 OPC 컴포넌트 추가 시 이 리뷰의 분류 체계 참고

## 태그
`Recipe`, `IEEE`, `Review`, `DNN`, `GPU`, `CNN`, `GNN`, `GAN`, `Transformer`, `OPC`, `Deep Learning`, `cuLitho`, `2024`
