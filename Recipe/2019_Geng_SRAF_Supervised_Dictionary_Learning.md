# SRAF Insertion via Supervised Dictionary Learning

## 메타데이터
- **저자**: Hao Geng, Wei Zhong, Haoyu Yang, Yuzhe Ma, Joydeep Mitra, Bei Yu
- **연도**: 2019 (ASP-DAC 발표), 2020 (IEEE TCAD 게재)
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD), Vol. 39, No. 10, pp. 2849–2859
- **DOI/URL**: https://ieeexplore.ieee.org/document/8847330/
- **인용수**: ~50

## 핵심 요약
최신 SRAF 삽입 툴 대비 ML 모델 성능과 마스크 최적화 품질(EPE, PV 밴드 면적)을 모두 향상시키는 감독 사전 학습(Supervised Dictionary Learning) 기반 SRAF 삽입 프레임워크. 기존 수동 피처 구성을 강화하여 피처 추출과 차원 축소를 동시에 수행하는 온라인 사전 학습 알고리즘을 처음으로 제안한다. 사후 처리 단계에서 설계 규칙을 전역적으로 고려하는 정수 선형 프로그래밍(ILP) 모델을 적용한다.

## 주요 기여
1. 피처 추출과 차원 축소를 동시 수행하는 감독 온라인 사전 학습 알고리즘 (최초 적용)
2. SRAF 삽입 후처리를 위한 2개의 ILP(정수 선형 프로그래밍) 모델
3. 최신 SRAF 삽입 툴 대비 EPE 및 PV 밴드 면적 향상
4. 전역적 설계 규칙 고려 (패턴 간 SRAF 충돌 해결)

## Recipe/Process Flow 상세

### 감독 사전 학습 기반 SRAF 파이프라인
```
1. 피처 추출 (감독 사전 학습)
   - 입력: 레이아웃 패치 (주변 패턴 기하학 정보)
   - 감독 온라인 사전 학습:
     * 사전 D ∈ R^(n×k): k개의 원자(atom)
     * 희소 코드 α: x ≈ D·α (희소 표현)
     * 레이블 정보 활용 (SRAF 유무)로 판별적 사전 학습
     * 최소화: Σ [||xi - D·αi||² + λ||αi||₁ + γ·L(αi, yi)]
       여기서 L = 지도 손실 (레이블 일치)

2. 차원 축소
   - 고차원 레이아웃 피처 → 저차원 사전 기반 표현
   - 불필요한 정보 제거, 판별 정보 보존
   - 실시간 온라인 업데이트 가능

3. SRAF 분류 및 예측
   - 학습된 표현으로 SRAF 삽입 위치/크기 예측
   - SVM 또는 신경망 분류기 사용

4. ILP 후처리 (설계 규칙 전역 최적화)
   ILP 모델 1: SRAF 위치 선택
     - 목적: 공정 윈도우 메트릭 최대화
     - 제약: SRAF 간 최소 이격 (설계 규칙)

   ILP 모델 2: SRAF 크기 최적화
     - 목적: EPE 최소화
     - 제약: SRAF 폭 범위, MRC 규칙

5. 최종 SRAF 생성
   - ILP 결과로 전체 레이아웃 SRAF 최종 결정
   - DRC 검증
```

### 성능 결과 (최신 SRAF 툴 대비)
```
ML 모델 성능: 향상 (판별적 피처로 분류 정확도 개선)
EPE: 감소 (더 정확한 SRAF 위치/크기)
PV 밴드 면적: 증가 (공정 윈도우 확장)
전역 설계 규칙 준수: ILP로 충돌 없는 SRAF 보장
```

## OPC 툴 구현 관련성
- **SKOPC SRAF 모듈**: 사전 학습 기반 피처 표현은 `skopc/modeling/sraf_generator.py`에서 레이아웃 피처 인코딩에 활용 가능
- **ILP 후처리**: SRAF 충돌 해결을 위한 ILP는 대규모 레이아웃 SRAF 삽입의 필수 단계
- **온라인 학습**: 새 데이터에 점진적 적응 가능 — 노드 전환 시 재훈련 비용 절감
- **Bei Yu 그룹 (CUHK)**: CTM-SRAF, GAN-SRAF와 동일 그룹의 일관된 발전 계보

## 참고문헌
- IEEE TCAD Vol. 39, No. 10, 2020 (ASP-DAC 2019 발표)
- PDF: https://personal.hkust-gz.edu.cn/yuzhema/papers/C6-ASPDAC2019-SRAF.pdf
- 관련: GAN-SRAF (IEEE TCAD, 2020)
- 관련: CTM-SRAF (IEEE TCAD, 2023)
- 관련: Subresolution Assist Feature Generation With Supervised Data Learning (IEEE TCAD, 2018)

## 태그
`Recipe`, `IEEE`, `TCAD`, `SRAF`, `DictionaryLearning`, `MachineLearning`, `ILP`, `IntegerProgramming`, `DesignRules`, `Bei-Yu`, `CUHK`
