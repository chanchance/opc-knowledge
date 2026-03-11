# Generic Lithography Modeling with Dual-band Optics-Inspired Neural Networks

## 메타데이터
- **저자**: Haoyu Yang, Zongyi Li, Kumara Sastry, Saumyadip Mukhopadhyay, Mark Kilgard, Anima Anandkumar, Brucek Khailany, Vivek Singh, Haoxing Ren (NVIDIA)
- **연도**: 2022
- **게재지/학회**: DAC 2022 (59th Design Automation Conference) / arXiv:2203.08616
- **DOI/URL**: https://arxiv.org/abs/2203.08616
- **인용수**: 다수 인용

## 핵심 요약
리소그래피 시뮬레이션을 위한 이중 밴드 광학 영감 신경망 아키텍처로, VLSI 설계의 계산 병목을 해결한다. 1nm²/픽셀 해상도에서 임의 크기 타일의 비아/금속층 윤곽 시뮬레이션 최초 달성이라는 이정표를 세웠다. 이전 ML 솔루션 대비 모델 크기 20배 감소, 전통적 시뮬레이터 대비 85배 속도 향상을 이루면서 99% 이상 정확도를 유지한다.

## 주요 기여
- **최초 달성**: 1nm²/픽셀 해상도에서 임의 크기 타일로 비아/금속층 윤곽 시뮬레이션 최초 발표
- **85배 속도 향상**: 전통적 시뮬레이터 대비 85배 빠른 추론 (1% 정확도 손실)
- **20배 모델 크기 감소**: 이전 ML 솔루션 대비 20배 작은 모델
- **이중 밴드 광학 영감 설계**: 리소그래피의 광학 물리학을 고려한 신경망 아키텍처

## Recipe/Process Flow 상세

### 이중 밴드 광학 영감 아키텍처

**광학 물리학 기반 설계**
리소그래피 이미징에서 두 가지 주파수 밴드 역할:
1. **저주파 밴드**: 전체 패턴의 글로벌 조명 및 회절 특성
2. **고주파 밴드**: 에지 및 코너의 세밀한 광학 근접 효과

이중 밴드 접근으로 기존 단일 해상도 접근법의 한계 극복:
- 다양한 피처 크기에서 정확한 윤곽 예측
- 광학 물리학 원리를 아키텍처에 내장

### 리소그래피 시뮬레이션 파이프라인

**입력**: IC 레이아웃 타일 (임의 크기 지원)

**단계 1: 저주파 경로 처리**
- 대규모 영역의 글로벌 조명 및 회절 효과 포착
- 낮은 해상도에서 전체 패턴 특성 인코딩

**단계 2: 고주파 경로 처리**
- 에지 및 코너의 세밀한 광학 근접 효과 포착
- 높은 해상도에서 지역 패턴 세부사항 인코딩

**단계 3: 이중 밴드 융합**
- 저주파 + 고주파 경로 정보 결합
- 1nm²/픽셀 해상도의 최종 윤곽 예측

**출력**: 시뮬레이션된 레지스트 윤곽 (1nm²/픽셀)

### OPC 통합 흐름
1. 레이아웃 타일 입력
2. 듀얼밴드 신경망으로 빠른 리소그래피 시뮬레이션
3. 예측 윤곽과 목표 패턴 비교
4. EPE 계산 및 OPC 보정 결정
5. OPC 보정 적용 후 재시뮬레이션 (선택적)
6. 최종 OPC 마스크 생성

### 성능 벤치마크
| 지표 | 값 |
|------|-----|
| 해상도 | 1nm²/픽셀 |
| 타일 크기 | 임의 크기 지원 |
| 속도 향상 | 전통적 시뮬레이터 대비 85× |
| 정확도 | 99%+ |
| 모델 크기 감소 | 이전 ML 대비 20× |

## OPC 툴 구현 관련성
- **빠른 OPC 시뮬레이터**: SKOPC의 LithoEngine에서 물리 시뮬레이터 대안으로 듀얼밴드 신경망 활용
- **임의 크기 타일 처리**: 다양한 OPC 레시피 레이아웃 크기에 유연하게 적응
- **1nm 해상도 시뮬레이션**: 고급 기술 노드 OPC 레시피의 정밀 시뮬레이션 지원
- **NVIDIA cuLitho 통합**: NVIDIA 팀 연구로 cuLitho 플랫폼과 통합 가능
- **OPC 레시피 반복 최적화**: 빠른 시뮬레이션으로 OPC 레시피 반복 최적화 루프 가속

## 참고문헌 (핵심)
- Yang et al. (2022): CFNO (arXiv:2207.04056) - 동일 저자 후속 연구
- Li et al. (2021): Fourier Neural Operator
- DAMO (Chen et al., 2020)
- LithoBench 벤치마크

## 태그
`Dual-band`, `Optics-Inspired`, `Lithography Simulation`, `Contour Prediction`, `1nm Resolution`, `85x Speedup`, `Via Layer`, `Metal Layer`, `NVIDIA`, `Recipe`, `OPC`, `DAC2022`, `Neural Network`
