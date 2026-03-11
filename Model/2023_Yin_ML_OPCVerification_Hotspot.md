# Machine Learning Assisted Effective OPC Verification Hotspot Capture

## 메타데이터
- **저자**: Lianghong Yin, Marko Chew, Shumay Shang, Le Hong, Fan Jiang, Ilhami Torunoglu
- **연도**: 2023
- **게재지**: Proc. SPIE 12751, Photomask Technology 2023
- **DOI/URL**: https://doi.org/10.1117/12.2687752

## 핵심 요약
Siemens EDA Calibre ML 기반 OPC 검증 툴을 활용하여 단일 제약 조건(constraint)으로 전체 레이아웃에서 모든 종류의 핫스팟(hotspot)을 효과적으로 캡처하는 방법을 제안한다. ML 분류기(classifier)를 통한 패턴 구분과 분류 제한 함수(classification limiting function)를 통한 출력 데이터 볼륨 제어가 핵심이다.

## 주요 기여
- ML 분류기를 활용한 OPC 검증 핫스팟 캡처의 효율화
- 단일 제약 조건으로 전체 레이아웃 내 모든 실패 메커니즘의 핫스팟 캡처
- 분류 제한 함수(classification limiting function)를 통한 출력 데이터 볼륨 제어
- 실제 핫스팟 누락 없이 검증 레시피 설정 및 엔지니어링 워크로드 대폭 간소화
- OPC 검증 정확도 향상과 동시에 false positive 감소

## 모델 수식/아키텍처
- ML 분류기: OPC 검증 결과의 패턴 유형 분류
- Classification limiting function: 클래스별 출력 데이터 양 조절
- Siemens EDA Calibre 플랫폼 기반 통합 워크플로우
- Failing mechanism별 단일 constraint → ML 분류기 → 핫스팟 리스트

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [x] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 검증(verification) 단계의 핫스팟 캡처 효율화에 직접 활용
- SKOPC의 OPC 검증 모듈에서 ML 기반 핫스팟 분류 통합 가능
- full-chip OPC 검증에서의 엔지니어링 부담 감소 방향과 일치

## 태그
`Model`, `SPIE`, `OPC Verification`, `Hotspot`, `Machine Learning`, `Classifier`, `Calibre`, `Full-Chip`
