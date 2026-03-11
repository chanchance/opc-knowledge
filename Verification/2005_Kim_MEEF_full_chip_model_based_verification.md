# Full-Chip Level MEEF Analysis Using Model Based Lithography Verification

## 메타데이터
- **저자**: Juhwan Kim, Lantian Wang, Daniel Zhang, Zongwu Tang
- **연도**: 2005
- **게재지**: Proc. SPIE 5992, 25th Annual BACUS Symposium on Photomask Technology, 59922U
- **DOI/URL**: https://doi.org/10.1117/12.632019
- **인용수**: 다수 (MEEF 전칩 분석 분야 선구적 논문)

## 핵심 요약
MEEF(Mask Error Enhancement Factor)는 서브-해상도 시대 이후 CD 균일성 제어의 핵심 인자이나, 긴 시뮬레이션 시간으로 인해 기존 연구는 소규모 패턴 영역에 국한되었다. 본 논문은 전칩(full-chip) 수준에서 마스크 오류가 웨이퍼 리소그래피 패터닝에 미치는 영향을 검증하기 위한 두 가지 실용적 방법론을 소개한다.

## 주요 기여
1. 전칩 MEEF 분석을 위한 두 가지 새로운 방법론 제시 — 기존 소규모 분석의 한계 극복
2. 모델 기반 리소그래피 검증(Model-Based Lithography Verification)을 마스크 sign-off에 적용 가능한 수준으로 확장
3. MEEF의 공간적 분포를 전칩 레이아웃에서 체계적으로 맵핑하는 기법 개발
4. 마스크 테이프아웃 전 마스크 오류 영향도를 정량화하는 실용적 프레임워크 확립

## 검증 방법론
- **모델 기반 전칩 시뮬레이션**: 웨이퍼 패터닝 물리 방정식(광학 이미징 + 레지스트 현상)을 효율적으로 풀어 전칩 검증에 적용
- **MEEF 계산**: 마스크 CD 변동 대비 웨이퍼 CD 변동 비율 `MEEF = dCDwafer / dCDmask`로 정의, 각 엣지 세그먼트별 산출
- **두 가지 방법론**:
  1. 전칩 레이아웃에서 고-MEEF 패턴 위치를 자동 식별하고 위험도 분류
  2. 공정 라티튜드(Process Latitude) 분석과 MEEF를 결합한 복합 검증 지표 활용
- **알고리즘**: TCC(Transmission Cross Coefficient) 기반 광학 모델 + 컴팩트 레지스트 모델

## 검증 지표
- EPE 허용 범위: MEEF와 마스크 CD 오차를 곱한 웨이퍼 CD 오차가 ±10% CD 이내
- 시뮬레이터: 모델 기반 리소그래피 검증 엔진 (Anchor 계열 툴)
- 커버리지: 전칩 레벨 — 0.13um, 0.11um, 90nm 노드 검증 데이터베이스 사용

## OPC 툴 구현 관련성
- **MEEF 계산 모듈 구현 직접 참조**: `VerificationEngine`에서 각 엣지 세그먼트의 MEEF 값을 산출하고 임계값 초과 엣지를 핫스팟으로 플래그하는 로직 설계에 활용
- 전칩 리소그래피 시뮬레이션 기반 마스크 sign-off 플로우의 알고리즘 구조 제공
- MEEF 기반 CD 오차 전파 분석으로 마스크 오차 허용 기준(MTE, Mask Tolerance Error) 설정 방법 제공
- OPC 후 검증(post-OPC verify) 단계에서 MEEF 체크를 추가하는 구현 근거

## 참고문헌
- SPIE BACUS Photomask Technology 2005, Vol. 5992
- 후속 전칩 MEEF 관련 연구 다수 인용

## 태그
`Verification`, `SPIE`, `MEEF`, `FullChip`, `MaskVerification`, `ModelBased`, `MaskSignOff`, `CDControl`
