# OPC Model Building for EUV Lithography

## 메타데이터
- **저자**: Benjamin C. P. Ho, Jonathan Doebler, Ardavan Niroomand
- **연도**: 2019
- **게재지**: Proc. SPIE 11147, International Conference on Extreme Ultraviolet Lithography 2019
- **DOI/URL**: https://doi.org/10.1117/12.2531430

## 핵심 요약
EUV 리소그래피가 논리(logic) 공정에서 메모리 공정으로 확장되면서, DUV OPC 모델 빌딩 플로우와 비교하여 EUV 고유의 물리적 효과를 어떻게 OPC 모델에 통합하는지를 체계적으로 분석한 논문. 비텔레센트릭 조명에 의한 섀도잉(shadowing), 슬릿 방향 변화(across-slit variation), 광학 플레어(optical flare), 레티클 블랙 보더(reticle black border) 효과를 모두 모델에 반영하는 방법론을 제시하였다.

## 주요 기여
1. **DUV vs. EUV OPC 모델 빌딩 플로우 비교**: 두 기술 세대 간의 모델링 차이점을 체계적으로 정리
2. **EUV 고유 효과 모델링**: 섀도잉, 슬릿 방향 변화, 광학 플레어, 블랙 보더 효과를 모두 OPC 모델에 통합
3. **메모리 HVM(High Volume Manufacturing) 적용**: 메모리 양산에서 EUV OPC 모델 구축의 실용적 도전과 해결책 제시
4. **플레어 보정 통합**: EUV 플레어(scattered light)에 의한 패턴 밀도 의존 이미징 오차를 모델 내에서 정량적으로 처리하는 방법

## 검증 방법론
- EUV 리소그래피 노출 데이터를 활용한 OPC 모델 캘리브레이션 패턴 검증
- 슬릿 방향별(across-slit) CD 편차를 별도 파라미터로 추출하여 모델 정확도 평가
- DUV 대비 EUV 모델 잔차(residual) 비교로 신규 물리 항목의 기여 정량화
- 플레어 맵(flare map)을 기반으로 패턴 밀도 의존 오차를 시뮬레이션과 실제 웨이퍼 CD 간 비교

## OPC 툴 구현 관련성
- EUV OPC 모델 빌더에 비텔레센트릭 섀도잉 항목 추가 필요성 직접 제시
- 슬릿 위치 의존 보정(across-slit correction) 테이블 또는 함수를 모델 파라미터로 지원해야 함
- 플레어 보정 맵 연산 모듈(리소그래피 엔진 전처리 단계)의 설계 가이드라인
- SKOPC의 `LithoEngine` 및 OPC 캘리브레이션 모듈에서 EUV 지원 시 반드시 참조해야 하는 기초 문헌

## 태그
`Verification`, `SPIE`, `EUV`, `OPC Model`, `Flare`, `Shadowing`, `Model Calibration`, `HVM`
