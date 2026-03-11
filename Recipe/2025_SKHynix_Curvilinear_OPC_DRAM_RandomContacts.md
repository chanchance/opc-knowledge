# Improved Manufacturability in Curvilinear OPC for Random DRAM Contacts

## 메타데이터
- **저자**: SK Hynix Inc.
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 1342516
- **DOI/URL**: https://doi.org/10.1117/12.3051561

## 핵심 요약
랜덤 DRAM 컨택 레이어에 곡선형(curvilinear) OPC를 적용하여 제조성(manufacturability)을 향상시키는 방법을 제안한다. 피치 축소에 따라 DRAM 컨택 레이어에서 curvilinear OPC가 필수 기술로 부상하지만, 긴 런타임과 SRAF 프린팅 결함이 주요 과제다. ML 기반 OPC 모델과 고유 패턴 선택 방법을 결합하여 DOF 33% 이상 향상과 SRAF 프린트 결함 제거를 달성한다.

## 주요 기여
1. **DRAM 컨택 Curvilinear OPC**: 랜덤 DRAM 컨택 레이어 최초의 실용적 curvilinear OPC 구현
2. **DOF 33%+ 향상**: 기존 rectilinear OPC 대비 DOF(Depth of Focus) 33% 이상 향상
3. **SRAF 프린트 결함 제거**: 공격적인 curvilinear SRAF 배치에서 SRAF 프린팅 결함 없음
4. **ML 기반 OPC 모델**: ML OPC 모델로 초기 보정 후 수렴 엔진 fine-tuning 하이브리드 플로우
5. **고유 패턴 선택 방법**: full-chip에서 고유 패턴 세트를 식별하는 새 패턴 선택 방법 개발

## Recipe/Flow 상세
- **DRAM 컨택 Curvilinear OPC 플로우**:
  1. **고유 패턴 선택**:
     - 전체 칩 DRAM 컨택 레이아웃 분석
     - 유사한 패턴 환경 클러스터링
     - 각 클러스터에서 고유 대표 패턴 선택
     - 선택된 패턴에만 full curvilinear OPC 수행 → 런타임 단축
  2. **ML OPC 모델 적용**:
     - ML 모델로 각 패턴에 대한 초기 curvilinear 보정량 예측
     - 곡선 SRAF 위치 및 크기 ML 예측
     - 수렴 엔진 입력으로 ML 예측 결과 사용
  3. **Curvilinear OPC 수렴**:
     - ML 초기값에서 시작하여 최적화 반복
     - MRC(Mask Rule Check) 준수 curvilinear 폴리곤 생성
     - 수렴 조건: EPE, SRAF 프린팅 없음, DOF 최대화
  4. **SRAF 프린팅 검증**:
     - 레지스트 모델로 SRAF 프린팅 시뮬레이션
     - 프린팅 위험 SRAF 크기/위치 조정
     - SRAF 크기를 MRC 한계 이상으로 안전하게 유지하면서 성능 최대화
  5. **DOF 최적화 검증**:
     - Focus-Exposure 매트릭스 시뮬레이션
     - Curvilinear vs. rectilinear OPC DOF 비교
     - 주요 임계 패턴에서 DOF 33%+ 향상 확인
- **DRAM 컨택 특수 고려사항**:
  - 랜덤 배치 컨택: 규칙적 어레이보다 다양한 패턴 환경
  - 고밀도 컨택: 인접 컨택 간 상호 근접 효과
  - EUV 스토케스틱: 컨택 크기에서 결함 확률 높음 → curvilinear로 완화
- **소속 기관**: SK Hynix Inc. (한국)

## OPC 툴 구현 관련성
- SKOPC DRAM 컨택 레이어 curvilinear OPC 모드 구현
- `dram_contact_curvilinear_opc.py`: 고유 패턴 선택 + ML OPC + 수렴 엔진 하이브리드
- SRAF 프린팅 검증 루프: 레지스트 시뮬레이션으로 SRAF 안전성 확인
- DRAM 컨택 DOF 최적화를 위한 curvilinear OPC 레시피 설계

## 태그
`CurvilinearOPC`, `DRAM`, `Contact`, `Memory`, `MachineLearning`, `SRAF`, `DOF`, `Manufacturing`, `SKHynix`, `SPIE`, `2025`
