# Novel End-to-End Production-Ready Machine Learning Flow for Nanolithography Modeling and Correction (TPM-RET)

## 메타데이터
- **저자**: Mohamed S. E. Habib, Hossam A. H. Fahmy, Mohamed F. Abu-ElYazeed
- **연도**: 2024
- **게재지/학회**: arXiv preprint, arXiv:2401.02536
- **DOI/URL**: https://arxiv.org/html/2401.02536v1
- **기관**: EECE, Faculty of Engineering, Cairo University, Egypt

## 핵심 요약
TPM-RET(True Pixel-based Machine learning Resolution Enhancement Technique)는 ML 기반 RET의 생산 적용을 막는 8가지 장애물을 분석하고, 이를 해결하는 엔드-투-엔드 CPU 네이티브 리소그래피 보정 플로우를 제시한다. 역강도 프로파일(IIP) 표현과 비균일 이미지 압축을 통해 128 코어에서 125배 속도 향상을 달성하며, 32nm 금속 레이어에서 OPC와 SRAF 보정을 동시에 수행한다.

## 주요 기여
- **IIP(역강도 프로파일) 표현**: 이진 마스크에서 공정 정보를 연속 강도 그래디언트로 복원하여 ML 모델의 물리 학습 향상
- **비균일 압축**: 리소그래피 비대칭성을 유지하며 2001×2001에서 250×250으로 입력 축소
- **CPU 네이티브 스케일링**: GPU 의존 없이 128 CPU 코어에서 97% 효율, 125배 가속
- **윈도우 스티칭 제거**: 픽셀 단위 처리로 타일 경계 불일치 아티팩트 완전 제거

## Recipe/Process Flow 상세

### TPM-RET 엔드-투-엔드 플로우

```
설계 레이아웃 입력
        ↓
[데이터 준비 단계]
  1. 설계 패턴 → 고해상도 이미지 변환
  2. Calibre pxOPC로 ILT 포토마스크 생성 (ground truth)
  3. 커널 컨볼루션으로 IIP 맵 계산:
     IIP(x,y) = ∫∫ K(x-x', y-y') · M(x',y') dx'dy'
  4. 2001×2001 이미지 → 250×250으로 비균일 압축
  5. IIP 값을 100개 클래스로 양자화 (분류 문제로 변환)
        ↓
[ML 모델 추론 (MobileNetV3)]
  - 경량 CNN으로 각 픽셀의 IIP 클래스 예측
  - 스케일링 매니저가 CPU 코어에 픽셀 분배
  - 128 코어 병렬 처리
        ↓
[IIP 맵 재구성]
  - 예측된 IIP 클래스에서 완전 IIP 맵 재구성
        ↓
[후처리]
  - IIP 맵에 임계값 적용 → 이진 포토마스크
  - SRAF 패턴 포함 최종 마스크 생성
        ↓
최종 보정 마스크 출력 (OPC + SRAF 동시 적용)
```

### IIP(역강도 프로파일) 표현 상세
- 목적: 이진 마스크의 공정 정보 손실 문제 해결
- 방법: 리소그래피 커널로 마스크를 컨볼루션하여 연속값 프로파일 생성
- 효과: ML 모델이 이진 패턴을 암기하는 대신 물리 원리 학습

수식:
$$IIP(x,y) = \sum_i K_i(x,y) * M(x,y)$$
- $K_i$: i번째 리소그래피 커널 (Hopkins 고유모드)
- $M$: 마스크 패턴

### ML 기반 RET 생산화 8가지 장애물
1. **마스크 정보 손실**: 이진 마스크 학습 데이터에서 공정 정보 소실 → IIP로 해결
2. **풀칩 스케일링**: 복잡한 스티칭 필요 → 픽셀 단위 처리로 해결
3. **보정 비일관성**: 윈도우 위치에 따른 변동 → 픽셀 레벨 통합으로 해결
4. **GPU 인프라 요구**: 기존 FAB 시스템과 비호환 → CPU 네이티브로 해결
5. **비대칭 패턴 상호작용**: 윈도우 경계에서 비대칭 → 비균일 압축으로 처리
6. **입력 해상도 트레이드오프**: 정확도 vs 계산 비용 → 비균일 압축으로 균형
7. **미학습 패턴**: 모델 재학습 필요 → IIP 기반 일반화 향상
8. **RET 보정 분할**: 불필요한 복잡성 → 엔드-투-엔드로 통합

### 성능 결과 (32nm 금속 레이어)
| 지표 | TPM-RET | 기존 방법 |
|------|---------|---------|
| CPU 스케일링 효율 | 97% (128코어) | 낮음 |
| 속도 향상 | 125× | - |
| 스티칭 아티팩트 | 없음 | 있음 |
| OPC+SRAF | 동시 처리 | 별도 |

### 학습 설정
- 훈련 데이터: 40nm 및 140nm 격리 라인/라인-스페이스 패턴
- 모델: MobileNetV3 (경량 CNN)
- 분류: 100개 IIP 클래스
- 검증: 32nm 금속 레이어 (미학습 치수)

## OPC 툴 구현 관련성
TPM-RET의 접근 방식은 SKOPC CPU 기반 배치 처리에 직접 적용 가능:
- **IIP 표현**: SKOPC 모델 OPC에서 리소그래피 커널 기반 IIP를 학습 특성으로 활용
- **CPU 스케일링**: recipe_runner.py의 배치 처리를 TPM-RET 방식의 CPU 병렬화로 최적화
- **OPC+SRAF 통합**: 별도 단계로 분리된 OPC/SRAF를 단일 ML 모델로 통합하는 구조 참조
- **픽셀 단위 처리**: GDS 타일 경계 처리 문제를 픽셀 레벨 통합으로 해결

## 참고문헌 (핵심)
- Calibre pxOPC (Siemens EDA ILT 도구)
- MobileNetV3: Howard et al., "Searching for MobileNetV3" (ICCV 2019)
- Hopkins, "On the diffraction theory of optical images" (1953)
- LithoBench (NeurIPS 2023)

## 태그
`TPM-RET`, `Production ML`, `OPC`, `SRAF`, `IIP`, `CPU Scalable`, `MobileNetV3`, `End-to-end`, `Pixel-based`, `32nm`, `Cairo University`, `2024`, `arXiv`
