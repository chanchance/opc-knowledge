# CTM-SRAF: Continuous Transmission Mask-Based Constraint-Aware Subresolution Assist Feature Generation

## 메타데이터
- **저자**: Ziyang Yu, Peiyu Liao, Yuzhe Ma, Bei Yu, Martin D.F. Wong
- **연도**: 2023
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD)
- **DOI/URL**: https://doi.org/10.1109/TCAD.2023.3239559
- **인용수**: ~30

## 핵심 요약
SRAFs(Sub-Resolution Assist Features)는 패턴 충실도 향상 및 공정 윈도우 확대를 위한 핵심 RET(Resolution Enhancement Technique)이다. 본 논문은 CTM(Continuous Transmission Mask)의 강도 분포를 활용하여 설계 규칙을 준수하는 SRAF를 생성하는 강건한 제약 인식(constraint-aware) 방법론인 CTM-SRAF를 제안한다.

## 주요 기여
1. CTM 강도 분포 기반 SRAF 위치 및 형상 가이드 방법론
2. SRAF 삽입을 이차 제약을 갖는 정수 프로그래밍(IP)으로 정형화
3. 고속 탐침 기반(probe-based) SRAF 형상 진화 알고리즘
4. 설계 규칙 완전 준수하면서 공정 윈도우 최대화

## Recipe/Process Flow 상세

### SRAF 생성 파이프라인
```
1. CTM 최적화
   - 연속 투과율 마스크(CTM) 최적화 수행
   - 전형적 ILT/SMO 솔버로 CTM 생성
   - 강도 분포 I_CTM(x,y) 추출

2. SRAF 후보 위치 결정
   - CTM 강도 분포에서 국소 극대값 탐색
   - SRAF 배치 적합 영역 = CTM 강도가 특정 임계값 이상인 영역
   - 기하학적 필터링: 주 패턴으로부터 최소 이격 거리 확인

3. 제약 인식 SRAF 삽입 (Integer Programming)
   - 목적함수: 공정 윈도우 지표 최대화
   - 제약조건 (이차 제약 포함):
     * 설계 규칙: SRAF 폭, SRAF 간격, SRAF-주패턴 간격
     * 마스크 제조 규칙: MRC(Mask Rule Check)
     * SRAF 인쇄 방지: SRAF 자체가 웨이퍼에 인쇄되지 않도록
   - 고속 알고리즘으로 IP 문제 효율적 풀이

4. 탐침 기반 SRAF 형상 진화
   - 초기 직사각형 SRAF에서 시작
   - 탐침(probe)이 SRAF 경계를 점진적 조정
   - CTM 강도 피드백으로 형상 최적화
   - Manhattan 또는 curvilinear SRAF 생성 가능

5. 검증
   - 리소그래피 시뮬레이션으로 최종 공정 윈도우 확인
   - EPE 측정 및 SRAF 인쇄 여부 확인
```

### 핵심 파라미터
- **CTM 강도 임계값** (θ_CTM): SRAF 후보 위치 결정
- **SRAF 최소/최대 폭**: 마스크 제조 규칙에서 결정
- **SRAF-주패턴 최소 이격**: 설계 규칙
- **탐침 이동 스텝 크기**: 형상 진화 해상도
- **IP 솔버 파라미터**: 최대 이터레이션, 허용 오차

### 성능 결과
- Rule-based SRAF 대비 공정 윈도우 면적 ~15% 향상
- 기존 model-based SRAF 대비 런타임 대폭 감소
- 설계 규칙 위반 없는 SRAF 생성 보장

## OPC 툴 구현 관련성
- **SKOPC SRAF 모듈**: `skopc/modeling/sraf_generator.py`에 CTM 기반 SRAF 삽입 알고리즘 구현 참조
- **ILT 연계**: OpenILT CTM 출력을 SRAF 가이드로 활용 가능
- **설계 규칙 통합**: IP 제약으로 DRC 규칙 자동 준수
- **Bei Yu 그룹**: CUHK-HKUST, 컴퓨테이셔널 리소그래피 주요 연구팀

## 참고문헌
- IEEE TCAD, October 2023
- 지원: Research Grants Council of Hong Kong, SAR, Project CUHK14208021
- 관련: SRAF rule extraction and insertion based on ILT (SPIE 10961, 2019)
- 관련: GAN-SRAF (IEEE TCAD, 2020)

## 태그
`Recipe`, `IEEE`, `TCAD`, `SRAF`, `CTM`, `IntegerProgramming`, `ConstraintAware`, `ProcessWindow`, `MaskOptimization`, `Bei-Yu`
