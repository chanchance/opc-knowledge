# Model-Based OPC Extension in OpenILT

## 메타데이터
- **저자**: (CUHK Bei Yu 그룹 - IEEE document 10617951)
- **연도**: 2024
- **게재지**: IEEE Conference Publication (ISEDA 2024)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10617951/
- **인용수**: 신규 논문

## 핵심 요약
오픈소스 컴퓨테이셔널 리소그래피 라이브러리인 OpenILT를 확장하여 Model-Based OPC(MB-OPC)를 지원하는 연구. MB-OPC는 수학적 모델로 이미지 형성 프로세스를 시뮬레이션하고 마스크 레이아웃을 조정하는 방법이다. GPU 가속을 통해 대규모 레이아웃에서의 MB-OPC 실용화를 달성하며, OpenILT 프레임워크 내에서 OPC와 ILT를 통합 운용할 수 있는 기반을 제공한다.

## 주요 기여
1. OpenILT 오픈소스 플랫폼에 MB-OPC 기능 통합 확장
2. GPU 가속 기반 대규모 레이아웃 MB-OPC 구현
3. 코너 세그먼트 파라미터 최적화를 포함한 세분화(segmentation) 전략
4. EPE 기반 품질 지표로 MB-OPC 수렴 평가 프레임워크

## Recipe/Process Flow 상세

### MB-OPC 기본 흐름 (OpenILT 확장)
```
1. 레이아웃 입력 및 세분화 (Segmentation)
   - 폴리곤 에지를 균일 세그먼트로 분할
   - uniform_length: 일반 에지 세그먼트 길이
   - corner_length: 코너 세그먼트 길이 (uniform보다 작게 설정)
     → 코너는 이미지 오차에 민감하여 더 세밀한 제어 필요

2. 광학 시뮬레이션
   - Hopkins 모델 기반 이미지 강도 계산
   - 레지스트 모델 적용
   - 웨이퍼 상 인쇄 패턴 예측

3. EPE 측정
   - 각 세그먼트의 목표 CD와 시뮬레이션 CD 비교
   - EPE threshold 초과 시 위반으로 분류
   - EPE 분포 통계 계산 (RMS, max, 3σ)

4. 마스크 업데이트 (이터레이션)
   - EPE 기반 세그먼트 이동량 계산
   - 댐핑 팩터 또는 PID 제어로 수렴 제어
   - 마스크 규칙(MRC) 위반 방지

5. GPU 가속
   - 대규모 레이아웃 병렬 처리
   - 수천만 세그먼트 동시 업데이트
   - CPU 대비 수십 배 속도 향상
```

### 세분화 파라미터 가이드라인
```
uniform_length: 50-100nm (노드에 따라 조정)
corner_length: 20-40nm (uniform의 30-50%)
최소 세그먼트 길이: DRC 규칙으로 결정
최대 세그먼트 수: 메모리/런타임 제약으로 결정
```

### EPE 평가 기준
```
EPE threshold: 노드별로 다름
  - 28nm 노드: ±3-5nm
  - 14nm 노드: ±2-3nm
  - 7nm 노드: ±1-2nm
수렴 기준: 전체 세그먼트의 99% 이상이 EPE threshold 이내
```

## OPC 툴 구현 관련성
- **SKOPC 직접 연관**: `skopc/modeling/openilt_adapter.py`의 ILT 인터페이스와 동일한 OpenILT 기반
- **오픈소스 확장**: OpenILT(2024_Zheng_OpenILT)의 MB-OPC 확장판으로, SKOPC에 직접 통합 가능
- **GPU 가속**: 대용량 칩 레이아웃 OPC에 필수적인 GPU 병렬화 방법론 제공
- **코너 처리**: 코너 세그먼트 전략은 2D 패턴 OPC 정확도 향상의 핵심

## 참고문헌
- IEEE ISEDA 2024, Document 10617951
- CUHK Bei Yu 그룹: https://www.cse.cuhk.edu.hk/~byu/papers/C209-ISEDA2024-ModelOPC.pdf
- 관련: OpenILT (2024_Zheng_OpenILT)
- 관련: Model-Based OPC With Adaptive PID Control (IEEE, 2025)

## 태그
`Recipe`, `IEEE`, `ModelBasedOPC`, `OpenILT`, `GPU-Acceleration`, `Segmentation`, `EPE`, `OpenSource`, `Bei-Yu`, `2024`
