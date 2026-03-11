# Affordable Optical Proximity Correction Runtime for EUV Curvilinear Mask Tape-out Flow

## 메타데이터
- **저자**: Ping Digaum, Kazuto Kajiwara, Nobue Kosa, Ming-Chuan Yang, Ezequiel Vidal Russell, Jianhong Qiu, Omar Ndiaye, Nicolas Martin, Hesham Omar, Ehsan Kabiri Rahani, Peigen Cao, Michael Crouse
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540T (10 April 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3009981

## 핵심 요약
EUV 곡선형(curvilinear) 마스크 테이프아웃 플로우를 위한 실용적인 OPC 런타임 프레임워크를 제시한다. 소스 최적화, OPC 및 검증 런타임, 마스크 근접 보정(MPC) 런타임, 데이터 볼륨 처리, 마스크 라이팅 시간 등 곡선형 EUV 마스크와 관련된 도전 과제를 해결하기 위해 여러 엔진의 기능을 연결하는 균형 잡힌 접근법을 제안한다.

## 주요 기여
1. **곡선형 마스크 테이프아웃 플로우**: 소스 최적화 → OPC → MPC → 검증의 통합 플로우
2. **런타임-정확도 균형**: 다양한 엔진 연결로 정확도와 마스크 TAT 균형 달성
3. **데이터 볼륨 처리**: 곡선형 마스크의 증가된 데이터 볼륨 관리 방법
4. **전체 EUV 테이프아웃 솔루션**: 소스 최적화부터 마스크 라이팅까지 전체 플로우 통합

## 알고리즘/수식
### 곡선형 마스크 테이프아웃 플로우
```
단계 1: 소스 최적화 (SMO)
  - 빠른 소스 최적화로 최적 조명 형상 결정
  - 곡선형 마스크 친화적 소스 형상 도출

단계 2: 곡선형 OPC
  - ML ILT 또는 곡선형 OPC로 마스크 패턴 생성
  - 곡선형 표현 (B-spline, Bezier 등)

단계 3: 검증 (Verification)
  - 시뮬레이션 기반 ORC (Optical Rule Check)
  - 공정 창 검증

단계 4: 마스크 근접 보정 (MPC)
  - e-beam 라이팅 근접 효과 보정
  - 곡선형 패턴의 MPC 특수 처리

단계 5: 데이터 처리 및 마스크 라이팅
  - 곡선형 데이터 압축 및 포맷 변환
  - 다중 빔 마스크 라이터(MBMW) 출력
```

### 런타임 균형 전략
```
엔진 선택 기준:
  빠른 모델 (빠른 OPC): 초기 마스크 생성, 전체 칩 적용
  엄격한 모델 (정확한 OPC): 핫스팟 및 약점 패턴 재최적화

데이터 볼륨 관리:
  곡선형 좌표 → 압축 표현 (Bezier/B-spline 제어점)
  목표: 맨해튼 OPC 대비 데이터 증가 최소화
```

## OPC 툴 SMO 구현 관련성
- EUV 곡선형 마스크 테이프아웃의 전체 플로우 설계 참조
- 소스 최적화가 테이프아웃 플로우 첫 단계임을 확인
- 런타임-정확도 트레이드오프: SKOPC에서 빠른 모드와 정밀 모드 분리 설계 지침
- MPC와 OPC의 통합: 마스크 제조 공정까지 고려한 플로우 설계

## 태그
`OPC`, `SMO`, `EUV`, `curvilinear_mask`, `tape_out`, `MPC`, `runtime`, `data_volume`, `MBMW`, `DTCO`, `SPIE`
