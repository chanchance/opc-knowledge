# Recent Advances in Computational Lithography Technology

## 메타데이터
- **저자**: (Springer Nature - Moore and More)
- **연도**: 2025
- **게재지**: Moore and More (Springer Nature), 2025
- **DOI/URL**: https://link.springer.com/article/10.1007/s44275-025-00032-5
- **인용수**: ~5

## 핵심 요약
계산 리소그래피 기술의 최근 발전을 포괄적으로 정리하는 리뷰 논문이다. OPC, ILT, SRAF, SMO, ML 기반 접근 등 주요 계산 리소그래피 방법의 최신 동향과 미래 방향을 다룬다. 반도체 공정 노드 축소에 따른 리소그래피 복잡성 증가와 이를 해결하기 위한 계산 방법의 발전을 체계적으로 분석한다.

## 주요 기여
1. OPC/ILT/SRAF/SMO 포함 계산 리소그래피 전 영역 최신 리뷰
2. AI/ML 기반 계산 리소그래피 방법 분류와 평가
3. EUV, High-NA EUV 리소그래피의 계산 과제 분석
4. 계산 리소그래피 미래 발전 방향 제시

## Recipe/Process Flow 상세

### 계산 리소그래피 영역 분류
```
1. 광학 근접 보정 (OPC):
   Rule-based OPC: 초기 방법, 단순, 빠름
   Model-based OPC (MB-OPC): 현재 주류, 정확
   AI-OPC: GNN, RL, 미분 가능 OPC → 빠름+정확
   커비리니어 OPC: 자유 형상 마스크 보정

2. 역 리소그래피 기술 (ILT):
   픽셀/레벨셋 기반: 전통적 수치 ILT
   GPU 가속 ILT: cuLitho, TorchLitho
   AI 기반 ILT: Neural-ILT, DevelSet, ILILT, L2O-ILT
   전체 칩 ILT: FuILT, POLY-GAN

3. 부해상 보조 피처 (SRAF):
   Rule-based SRAF: 테이블 기반
   Model-based SRAF: ILT 기반
   AI SRAF: GAN, RL, CTM, LLM 기반

4. 소스-마스크 최적화 (SMO):
   전통적 SMO: 가중합 방법
   다목적 SMO: NSGA-II 기반
   AI SMO: 딥러닝 기반 소스 최적화

5. ML 기반 접근:
   리소그래피 시뮬 가속: CNN/GAN 대리 모델
   핫스팟 탐지: CNN, Transformer, LLM
   모델 캘리브레이션: RL, ML 기반 게이지 선택
   레지스트 모델링: ML 기반 물리-데이터 혼합 모델
```

### EUV 특화 과제
```
EUV 리소그래피 (λ=13.5nm):
  마스크 3D 효과 (M3D): 비텔레센트리시티, 포커스 시프트
  확률론적 효과: 광자 샷 노이즈, LWR, LCDU, 실패율
  SRAF: EUV 반사형 마스크 SRAF 제약
  레지스트: EUV 레지스트 3D 반응 모델링

High-NA EUV (NA=0.55):
  아나모픽 광학: 4×/8× 비대칭 축소 → 마스크 에러 비대칭
  M3D 심화: 더 높은 NA → 더 큰 M3D 효과
  DOF 감소: 높은 NA → DOF 축소 → SMO 필요성 증가
  새로운 마스크 요구: 새로운 흡수체 재료, 두께

AI 기반 EUV 해결책:
  CNN/GAN EUV 시뮬: M3D 효과 빠른 예측
  확률론적 OPC (ST-OPC): 실패율 직접 최소화
  EUV SMO: 소스-마스크 동시 최적화
```

### 미래 발전 방향
```
파운데이션 모델:
  범용 마스크 최적화 사전 훈련 모델
  다양한 노드/레이어에 미세 조정으로 적응

생성 AI:
  LLM 기반 SRAF/OPC 생성 (LLM-SRAF)
  디퓨전 모델 기반 마스크 최적화

물리-AI 통합:
  물리 내재 신경망: 미분 방정식 + 데이터
  디지털 트윈: 실제 리소그래피 → 신경 시뮬

하드웨어 발전:
  GPU/TPU 가속 OPC: cuLitho 확장
  양자 컴퓨팅: 조합 최적화 가속 (장기)

High-NA EUV 계산:
  아나모픽 OPC: 4×/8× 비대칭 마스크 보정
  새로운 M3D 모델: High-NA 특화 EMF 모델
  확률론적 High-NA: 더 작은 DOF + 샷 노이즈
```

## OPC 툴 구현 관련성
- **SKOPC 전략**: 이 리뷰의 계산 리소그래피 분류로 SKOPC 모듈 커버리지 확인
- **방법 선택**: 각 영역(OPC/ILT/SRAF/SMO)별 최선 방법 선택 기준
- **EUV 확장**: SKOPC EUV 지원 확장 시 M3D, 확률론적 효과 모델링 참고
- **로드맵**: LLM/파운데이션 모델 등 미래 기능 로드맵에 활용

## 참고문헌
- Moore and More (Springer Nature), 2025
- DOI: https://doi.org/10.1007/s44275-025-00032-5
- 관련: AI ILT review (Light: Science & Applications, 2025)
- 관련: Large-scale VLSI mask optimization survey (IWAPS 2025)

## 태그
`Recipe`, `SpringerNature`, `Review`, `Survey`, `ComputationalLithography`, `OPC`, `ILT`, `SRAF`, `SMO`, `EUV`, `HighNA`, `MachineLearning`, `AI`, `2025`
