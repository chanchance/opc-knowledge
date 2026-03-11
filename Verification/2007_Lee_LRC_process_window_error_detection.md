# LRC Techniques for Improved Error Detection Throughout the Process Window

## 메타데이터
- **저자**: Venson Lee, Sheng-Hua Tsai, Jun Zhu, Lantian Wang, Shu-Mei Yang, Dan White
- **연도**: 2007
- **게재지**: Proc. SPIE 6730, Photomask Technology 2007, 67303F
- **DOI/URL**: https://doi.org/10.1117/12.746439
- **인용수**: 다수 (SPIE Photomask 분야 기준 논문)

## 핵심 요약
LRC(Lithography Rule Check)는 마스크 합성 플로우의 핵심 구성 요소로 자리잡았으나, 공정 복잡도 증가에 따라 요구사항도 높아졌다. 본 논문은 더 넓은 범위의 공정 조건에서 리소그래피 오류를 더 정밀하게 검출하기 위한 새로운 모델링·검사 기법을 제시한다. 공정 윈도우 기법을 통해 9개의 서로 다른 공정 포인트에서 잠재적 리소그래피 오류를 검사한다.

## 주요 기여
1. 9-포인트 공정 윈도우 기반 LRC 기법 도입 — 단일 공정 조건 대비 오류 검출 완성도 대폭 향상
2. 기존 LRC 대비 정확도(Accuracy)와 런타임 성능을 동시에 개선하는 새로운 모델링 기법 제안
3. 공정 윈도우 전반에 걸친 리소그래피 오류 검출의 완전성(Coverage) 향상 방법론 제시
4. 마스크 테이프아웃 전 sign-off 검증 단계에서 실용 가능한 수준의 런타임 확보

## 검증 방법론
- **9-포인트 공정 윈도우 검사**: Best Focus/Nominal Dose 중심으로 포커스·노광량 변동 조합 9개 포인트에서 시뮬레이션 수행
- **모델 기반 LRC**: 컴팩트 리소그래피 모델을 이용한 웨이퍼 윤곽선(contour) 시뮬레이션으로 에러 검출
- **허용 기준**: EPE(Edge Placement Error) 한계값 초과 여부를 기반으로 핫스팟 분류
- **알고리즘**: 공정 윈도우 내 최악 조건(worst-case) 컨투어를 추출하여 마진 평가

## 검증 지표
- EPE 허용 범위: 공정 노드별 CD 허용 범위에 준함 (sub-90nm 대상)
- 시뮬레이터: 모델 기반 LRC 엔진 (컴팩트 광학·레지스트 모델)
- 커버리지: 9-포인트 공정 윈도우 전체 검사 (포커스·노광 변동 포함)

## OPC 툴 구현 관련성
- **OPC Verification 컴포넌트의 핵심 알고리즘**: 공정 윈도우 기반 LRC 루프 구현 시 직접 참조 가능
- 9-포인트 공정 윈도우 검사는 `VerificationEngine`의 PVB(Process Variation Band) 검사에 바로 적용 가능
- EPE 한계값 기반 핫스팟 분류 로직 구현의 기준 방법론 제공
- 마스크 tape-out 전 sign-off 검증 플로우 설계 시 구조적 참조

## 참고문헌
- SPIE Photomask Technology 2007, Vol. 6730
- 관련 LRC/OPC 검증 후속 연구들 (Miyagi 2011, Yoo 2011 등)

## 태그
`Verification`, `SPIE`, `LRC`, `ProcessWindow`, `EPE`, `Hotspot`, `MaskSignOff`, `ModelBasedLRC`
