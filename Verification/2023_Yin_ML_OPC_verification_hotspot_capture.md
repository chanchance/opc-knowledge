# Machine Learning Assisted Effective OPC Verification Hotspot Capture

## 메타데이터
- **저자**: Lianghong Yin, Marko Chew, Shumay Shang, Le Hong, Fan Jiang, Ilhami Torunoglu
- **연도**: 2023
- **게재지**: Proc. SPIE 12751, Photomask Technology 2023, 127510W
- **DOI/URL**: https://doi.org/10.1117/12.2687752
- **인용수**: 신규 논문 (Siemens EDA, SPIE Photomask 2023)

## 핵심 요약
Siemens EDA Calibre의 ML 보조 OPC 검증 툴을 사용하여 핫스팟을 포착하는 방법을 제시한다. 각 실패 메커니즘에 대해 단일 제약 조건만으로 핫스팟을 포착하고, 패턴 차별화를 ML 분류기가 수행하며, 미조정 제약 조건 대신 분류 제한 함수(classification limiting functions)로 출력 데이터 볼륨을 제어한다. 이를 통해 레시피 설정을 단순화하면서 핫스팟 포착의 효율성을 향상시킨다.

## 주요 기여
1. ML 분류기 기반 OPC 검증 핫스팟 포착 — 단일 제약 조건으로 다양한 실패 패턴 커버
2. 분류 제한 함수(classification limiting functions)로 출력 데이터 볼륨 최적화
3. OPC 검증 레시피 설정 복잡도 대폭 감소 — 수동 임계값 튜닝 필요성 제거
4. Calibre ML-assisted OPC 검증 툴의 실무 적용 방법론 실증

## 검증 방법론
- **ML 분류기 구조**:
  - 입력: 각 패턴 세그먼트 주변의 이미지/레이아웃 특징 (공간 컨텍스트 포함)
  - 출력: 핫스팟 클래스 분류 (비아 개방, 브리지, 라인 핀치, 라인 브레이크 등)
- **단일 제약 조건 접근법**: 실패 메커니즘별로 하나의 물리 제약 조건만 정의, ML이 패턴 유형별 차별화 담당
- **분류 제한 함수**: 예측 신뢰도 임계값을 적용하여 false positive를 줄이고 출력 볼륨 제어
- **훈련 데이터**: 기존 OPC 검증 결과로 레이블링된 핫스팟/비핫스팟 패턴 쌍
- **평가 지표**:
  - 핫스팟 포착률(Capture Rate): ML 분류기가 실제 핫스팟을 검출하는 비율
  - False Positive Rate: 비핫스팟을 핫스팟으로 오분류하는 비율
  - 출력 데이터 볼륨 (보고된 핫스팟 수)

## 검증 지표
- EPE 허용 범위: Photomask 기술 노드 기준 (실패 메커니즘별 물리 제약 조건)
- 시뮬레이터: Siemens EDA Calibre ML-assisted OPC 검증 엔진
- 커버리지: 전칩 레이아웃 — ML 분류기로 전체 패턴 처리

## OPC 툴 구현 관련성
- **ML 기반 OPC 검증 모듈 구현의 최신 참조**: `VerificationEngine`에 ML 분류기를 통합하여 기존 물리 모델 기반 LRC의 false positive를 줄이고 레시피 설정을 단순화하는 아키텍처 설계에 직접 활용
- 단일 물리 제약 + ML 분류의 하이브리드 검증 파이프라인 구현 방법론 제공
- 출력 볼륨 제어를 위한 분류 신뢰도 임계값 기반 필터링 로직 구현 근거
- Calibre ML OPC 검증과의 상호 운용성(호환 데이터 형식) 이해에 유용

## 참고문헌
- SPIE Photomask Technology 2023, Vol. 12751
- Siemens EDA Calibre ML-assisted OPC verification 기술 문서

## 태그
`Verification`, `SPIE`, `MachineLearning`, `OPCVerification`, `Hotspot`, `Classifier`, `Calibre`, `PatternCapture`, `LRC`, `PostOPC`
