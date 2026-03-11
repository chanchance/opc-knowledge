# Using Pattern Analysis to Improve Process Window Qualification Cycle Time

## 메타데이터
- **저자**: Tsung-Wei Lin, Hung-Yu Lin, Meng-Shiun Chiang, Jung-Kuan Huang, Jason Sweis, Philippe Hurat, Chung-Chen Hsu, Chun-Sheng Wu, Chao-Yi Huang, Ya-Chieh Lai
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129541B
- **DOI/URL**: https://doi.org/10.1117/12.3009892
- **인용수**: 신규 논문 (Winbond + Cadence, SPIE Advanced Lithography 2024)

## 핵심 요약
PWQ(Process Window Qualification)는 IC 제조의 리소그래피 공정 윈도우를 검증하는 데 사용되는 잘 알려진 웨이퍼 검사 기법이다. Winbond OPC 팀과 Cadence Pegasus DFM 팀이 패턴 분석 플로우를 사용하여 PWQ 런타임과 정확도를 향상시키는 프로젝트를 진행했다. 이 플로우는 결함 데이터 전처리, 분류, 필터링을 포함하며, CD-SEM 이미지 자동 정렬로 추출 위치와 웨이퍼 결과를 개선한다.

## 주요 기여
1. 패턴 분석 기반 PWQ 런타임 단축 — 기존 PWQ 사이클 타임 개선
2. 결함 데이터 전처리·분류·필터링 자동화 플로우 구축
3. CD-SEM 이미지 자동 정렬로 추출 위치 정확도 향상
4. Winbond 양산 환경에서 실증 — 메모리 제조 공정 적용

## 검증 방법론
- **PWQ 플로우 개요**:
  - 포커스·노광량 행렬(FEM) 웨이퍼 노광으로 공정 윈도우 탐색
  - 웨이퍼 검사로 결함 위치 식별
  - 결함 패턴 분류로 공정 윈도우 한계 패턴 특성화
- **패턴 분석 플로우 구성**:
  1. 결함 데이터 전처리: 웨이퍼 검사 결과 정제 및 노이즈 제거
  2. 결함 분류: 패턴 유형별 분류 (핀치, 브리지, 라인 끊김 등)
  3. 결함 필터링: 관심 패턴 선택적 집중으로 분석 효율 향상
  4. CD-SEM 자동 정렬: 결함 위치의 SEM 이미지를 레이아웃에 정밀 정렬
- **정확도 평가**: 개선된 플로우 vs. 기존 PWQ의 결함 포착 정확도 비교
- **사이클 타임 측정**: 전체 PWQ 소요 시간 비교 (런타임 개선량)

## 검증 지표
- EPE 허용 범위: PWQ 공정 윈도우 한계 패턴 기준 (Winbond 메모리 공정)
- 시뮬레이터: Cadence Pegasus DFM 패턴 분석 툴
- 커버리지: 전칩 PWQ 결함 데이터 + CD-SEM 측정 데이터

## OPC 툴 구현 관련성
- **PWQ 기반 OPC 검증 사이클 단축**: `VerificationEngine`의 PWQ 연동 플로우 설계 시 패턴 분류·필터링 자동화로 사이클 타임을 단축하는 아키텍처에 직접 참조
- 결함 분류 알고리즘은 OPC 검증 결과를 패턴 유형별로 자동 그룹화하는 구현에 활용 가능
- CD-SEM 자동 정렬 방법론은 OPC 검증 모델 캘리브레이션의 측정 데이터 수집 파이프라인 개선에 활용
- 메모리 제품 OPC 검증 플로우 설계 시 PWQ 통합 방법의 최신 실무 기준

## 참고문헌
- SPIE DTCO and Computational Patterning III 2024, Vol. 12954
- Winbond Electronics / Cadence Design Systems Pegasus DFM 기술 협력

## 태그
`Verification`, `SPIE`, `PWQ`, `ProcessWindow`, `PatternAnalysis`, `CycleTime`, `CDSEM`, `DefectClassification`, `Filtering`, `Memory`, `Cadence`
