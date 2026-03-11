# A Novel Flow of Full-Chip OPC Model Calibration and Verification by Utilizing SEM Image Contours

## 메타데이터
- **저자**: Yuan Gan, Changlian Yan, Mengqing Yu, Penghui Zhu, Jing Qiao, Lile Lu, Shengrui Zhang, Ming Ding, Chunying Han, Weijie Shi, Xiaojun Luo, Junhai Jiang, Zongchang Yu
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540K
- **DOI/URL**: https://doi.org/10.1117/12.3010034

## 핵심 요약
기존 CD(Critical Dimension) 기반 OPC 모델 캘리브레이션의 대안으로 부상하는 SEM 이미지 윤곽(contour) 기반 OPC 모델링에서, 최종 캘리브레이션 모델의 품질을 향상시키는 혁신적인 full-chip 플로우를 제안한다. SEM 이미지 윤곽을 이용하여 OPC 모델 캘리브레이션과 검증을 통합적으로 개선한다.

## 주요 기여
1. **SEM 윤곽 기반 OPC 모델 캘리브레이션 개선**: 기존 CD 포인트 대비 윤곽 전체를 활용한 더 풍부한 학습 데이터
2. **Full-chip 플로우 통합**: 캘리브레이션과 검증을 하나의 통합 플로우로 연결
3. **모델 품질 향상**: SEM 윤곽의 공간적 정보를 완전히 활용하여 OPC 모델 정확도 개선
4. **혁신적 접근법**: 기존 sparse CD 측정 대비 dense 윤곽 정보로 다양한 2D 패턴 형상 캡처
5. **검증 강화**: 캘리브레이션에 사용된 것과 동일한 윤곽 데이터로 모델 검증 일관성 향상

## Recipe/Flow 상세
- **SEM 윤곽 기반 OPC 모델 캘리브레이션 플로우**:
  1. **SEM 이미지 수집**:
     - 다양한 패턴 타입 (line/space, contact, 2D 형상) SEM 이미지 촬영
     - 리소 후(resist) 및 etch 후 SEM 이미지 획득
  2. **윤곽 추출 및 전처리**:
     - SEM 이미지에서 패턴 윤곽선 자동 추출
     - 노이즈 제거, 스무딩, 품질 필터링
  3. **윤곽 기반 캘리브레이션**:
     - 기존: 이산 CD 포인트 → 새로운: 연속 윤곽 곡선
     - 목적함수: 시뮬레이션 윤곽 vs. SEM 윤곽 전체 형상 오차 최소화
     - 2D 코너, 라인엔드 등 복잡 형상도 캘리브레이션에 반영
  4. **Full-chip 검증**:
     - 캘리브레이션된 모델로 full-chip OPC 수행
     - 독립 SEM 측정으로 모델 검증
  5. **모델 품질 평가**: 윤곽 기반 RMS 오차, 2D 형상 오차 분포

- **SEM 윤곽 vs. CD 포인트 비교**:
  - CD 포인트: 미리 정의된 측정 위치의 1D 거리값 (sparse)
  - SEM 윤곽: 전체 패턴 경계 곡선 (dense, 2D 형상 정보 포함)
- **장점**: 코너 라운딩, 라인엔드 단축 등 2D 효과 더 정확히 캡처
- **적용 기술**: 첨단 로직/메모리 노드

## OPC 툴 구현 관련성
- SKOPC의 OPC 모델 캘리브레이션 모듈을 SEM 윤곽 기반으로 확장
- `opc_calibration.py`: CD 기반 + 윤곽 기반 하이브리드 캘리브레이션 구조
- SEM 윤곽 추출 파이프라인과 OPC 모델 피팅 연동
- 2D 패턴 형상 오차 기반 목적함수 구현

## 태그
`OPC`, `ModelCalibration`, `SEM`, `Contour`, `FullChip`, `2D`, `Verification`, `SPIE`, `2024`
