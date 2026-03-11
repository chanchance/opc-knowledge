# Full Field Stitching-Aware High-NA EUV OPC/RET Flow

## 메타데이터
- **저자**: Zachary Levinson, Yunqiang Zhang, Linghui Wu, Kai-Hsiang Chang, Shaowen Gao, Kevin Yang, Andy Dawes, Kevin Lucas
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250H
- **DOI/URL**: https://doi.org/10.1117/12.3052709

## 핵심 요약
High-NA EUV 리소그래피(0.55NA)에서 아나모픽 렌즈의 비대칭 축소율(X: 4×, Y: 8×)로 인해 동일 면적 노광을 위해 2회 이상의 스티칭(stitching) 노광이 필요하다. 이 논문은 전체 필드(full field) 스티칭을 고려한 High-NA EUV OPC/RET 플로우를 개발하고, 스티치 경계에서의 패터닝 제어를 위한 OPC 및 RET 옵션을 검토한다. 서브-해상도 보조 피처(AF) 및 서브-해상도 그리드(SRG) 배치 최적화로 스티칭 영역의 공정 창 및 이중 노광 효과를 제어한다.

## 주요 기여
1. **풀필드 스티칭 인식 OPC 플로우**: High-NA EUV 스티칭 영역을 포함한 전체 필드 OPC/RET 통합 플로우 개발
2. **스티치 영역 AF/SRG 최적화**: 스티칭 경계 공정 창 향상을 위한 보조 피처(AF) 및 서브-해상도 그리드(SRG) 배치 최적화
3. **이중 노광 효과 제어**: 스티칭 시 두 노광의 광학 근접 효과 상호작용 모델링 및 보정
4. **OPC/RET 옵션 비교**: 스티칭 친화적 패터닝을 위한 다양한 OPC 및 RET 전략 체계적 비교
5. **Synopsys Proteus 플랫폼 구현**: 업계 표준 OPC 툴에서 High-NA 스티칭 OPC 지원 구현

## Recipe/Flow 상세
- **High-NA EUV 풀필드 스티칭 OPC/RET 플로우**:
  1. **스티칭 필요성 및 과제**:
     - 0.55NA 아나모픽 렌즈: X방향 4× 축소, Y방향 8× 축소
     - 동일 칩 면적 커버에 X방향으로 2회 이상 스티칭 노광 필요
     - 스티칭 경계: 두 노광의 패턴이 만나는 영역 → 이중 노광 효과
     - OPC 정확도 과제: 경계에서의 광학 근접 효과 상호작용
  2. **스티칭 OPC 특수 고려사항**:
     - 공중 이미지 상호작용: 스티칭 경계의 두 노광 공중 이미지 중첩
     - 광학 근접 효과 상호작용: 경계 패턴의 이웃 환경 비대칭
     - 마스크 흡수체 반사율: 스티칭 영역 특수 패턴
     - 블랙 보더 근접 효과: 필드 경계 블랙 보더의 광학 영향
     - 인접 필드 산란광(stray light): 이웃 노광 필드의 기생 광
  3. **AF(Assist Feature) 배치 최적화**:
     - 스티칭 영역 공정 창(Focus Window) 향상을 위한 AF 배치
     - 경계부 패턴의 DOF(Depth of Focus) 확보
     - 비대칭 이웃 환경을 고려한 AF 크기/위치 조정
  4. **SRG(Sub-Resolution Grid) 최적화**:
     - 이중 노광 효과 감소를 위한 SRG 배치 전략
     - 스티칭 경계 인접 패턴의 CD 균일도 개선
     - SRG 형태(크기, 간격) 최적화
  5. **풀칩 스티칭 OPC 실행**:
     - 스티칭 경계 인식 OPC 엔진: 경계 패턴 특별 처리
     - 이중 노광 OPC 모델: 두 노광의 공동 OPC 최적화
     - ORC(Optical Rule Check)로 스티칭 영역 패터닝 검증
- **High-NA EUV 스티칭 OPC 전략 비교**:
  - 단일 마스크 스티칭 vs. 별도 마스크 스티칭 OPC
  - 스티칭 경계 위치 선택: 패턴 밀도 낮은 영역 선택
  - 스티칭 오버랩 폭 최적화
- **소속 기관**: Synopsys, Inc. (미국) + Synopsys Taiwan Co., Ltd. (대만)

## OPC 툴 구현 관련성
- SKOPC High-NA EUV 스티칭 OPC 모듈 설계 기준
- `stitching_aware_opc.py`: 스티칭 경계 인식 OPC 알고리즘 구현
- 스티칭 영역 이중 노광 광학 모델: 두 노광 공중 이미지 중첩 계산
- 아나모픽 렌즈(4×/8×) 비대칭 OPC 좌표 변환과 스티칭 통합

## 태그
`HighNA`, `EUV`, `0.55NA`, `Stitching`, `OPC`, `RET`, `AnamorphicLens`, `AssistFeature`, `SRG`, `DoubleExposure`, `FieldBoundary`, `Synopsys`, `SPIE`, `2025`
