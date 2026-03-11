# Etch Proximity Correction Through Machine-Learning-Driven Etch Bias Model

## 메타데이터
- **저자**: Seongbo Shim, Youngsoo Shin (KAIST)
- **연도**: 2016
- **게재지**: Proc. SPIE 9782, Advanced Etch Technology for Nanopatterning V, 97820O
- **DOI/URL**: https://doi.org/10.1117/12.2219057

## 핵심 요약
20nm DRAM 게이트 레이어에서 기계학습(ANN) 기반 에치 바이어스 모델로 에치 근접 보정(EPC)을 수행한다. 에치 바이어스 시뮬레이션의 풀칩 런타임 불가능 문제와 단순 룰의 정확도 한계를 ANN으로 해결하는 최초 시도 중 하나이다.

## 주요 기여
1. ANN 기반 에치 바이어스 모델을 EPC에 처음 적용한 선구적 연구
2. 기하학적 파라미터 + 광학 파라미터 조합으로 세그먼트 특성화
3. ANN 출력(에치 바이어스 예측)을 상용 OPC 툴에 통합
4. 20nm DRAM 게이트 레이어에서 실증 검증
5. 풀칩 레벨 에치 시뮬레이션의 런타임 문제를 ML로 해결하는 패러다임 제시

## 모델 수식/아키텍처
- **입력 특징 (관심 세그먼트 기술)**:
  - 기하학적: CD, pitch, 세그먼트 길이, 코너 각도, 근처 패턴 밀도
  - 광학: 공중 이미지 강도, 이미지 기울기(ILS), 도즈 마진
- **ANN 구조**: 완전 연결 다층 퍼셉트론
  - 입력층 → 은닉층(들) → 출력: 에치 바이어스 (nm)
- 학습 데이터: 에치 시뮬레이션 또는 SEM 측정 기반 에치 바이어스 레이블
- OPC 통합: ANN 예측 에치 바이어스를 OPC 툴의 에치 보정 테이블로 입력

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [x] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC EPC 모듈의 ML 기반 에치 바이어스 예측기 구현의 원조 참조 논문
- 기하학적 + 광학 특징 기반 에치 바이어스 ANN의 입력 설계 가이드
- Shin 그룹(KAIST)의 ML OPC/EPC 연구 시리즈 시작점
- `2021_Shin_CompLithoML_KAIST_Review.md`의 초기 핵심 연구
- `2021_Hooker_ML_EtchModel_OPC_ILT.md` 등 후속 ML 에치 연구의 기반

## 태그
`Model`, `Etch`, `EPC`, `ML`, `ANN`, `EtchBias`, `DRAM`, `OPC`, `KAIST`, `SPIE`
