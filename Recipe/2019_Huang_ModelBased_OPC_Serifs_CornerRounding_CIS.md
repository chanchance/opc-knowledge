# A Model-Based OPC Method to Add Serifs for Corner Rounding Design of CMOS Image Sensor

## 메타데이터
- **저자**: Zengzhi Huang, Lingyun Ni, Koichi Fujii, Xiaolu Huang
- **소속**: (SPIE Photomask Technology 2019 게재)
- **연도**: 2019
- **게재지**: Proc. SPIE 11148, Photomask Technology 2019, 1114813
- **DOI/URL**: https://doi.org/10.1117/12.2536495

## 핵심 요약
CMOS 이미지 센서(CIS) 픽셀 패턴에서 발생하는 코너 라운딩(corner rounding) 효과를 모델 기반 OPC serif 삽입으로 보정하는 방법을 제시한다. 기존 rule-based serif 방식 대신, 코너에 45도 방향으로 작은 사각형 타겟을 재설정(retargeting)한 후 model-based OPC를 실행하여 정밀한 serif 형상을 자동 생성한다.

## 주요 기여
1. **Model-based serif 생성**: 코너를 45도 방향 작은 직사각형으로 retargeting → model-based OPC 실행으로 serif 자동 생성
2. **Rule-based 대비 정밀도 향상**: 고정 크기의 rule-based serif 대신 패턴별 최적 serif 형상 산출
3. **CIS 픽셀 패턴 적용**: 정방형 픽셀 코너의 라운딩 보정으로 광수집 효율 개선
4. **45도 retargeting 기법**: 사각 코너에 대각선 방향 보조 타겟 설정으로 OPC 엔진이 serif를 자연스럽게 생성하도록 유도

## Recipe/Flow 상세
```
[Model-Based Serif OPC Flow]
1. 코너 식별:
   - 레이아웃에서 볼록 코너(convex corner) 위치 추출
   - 코너 각도 분류 (90도 직각 코너 대상)
2. Retargeting (45도 방향 타겟 재설정):
   - 각 코너에 45도 방향으로 작은 사각형 타겟 추가
   - 타겟 크기: 설계 규칙 및 serif 요구 크기 기반 설정
3. Model-Based OPC 실행:
   - 수정된 타겟(원본 + 45도 코너 타겟)으로 OPC 실행
   - OPC 엔진이 코너 타겟 충족을 위해 자동으로 serif 생성
4. Serif 형상 검증:
   - Serif 크기가 MRC(Mask Rule Check) 충족하는지 확인
   - 웨이퍼 시뮬레이션으로 코너 라운딩 보정 효과 검증
5. 전체 칩 적용 및 ORC
```

### 핵심 파라미터
- **Retargeting 각도**: 45도 (대각선 방향)
- **타겟 사각형 크기**: MRC 허용 범위 및 serif 요구 크기에 따라 결정
- **적용 대상**: 볼록 코너 (convex corner)
- **OPC 방식**: Model-based (resist 이미지 시뮬레이션 기반)

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: OPC 실행 전 코너 retargeting 전처리 단계 추가 참고
- `skopc/modeling/rule_opc.py`: rule-based serif 삽입을 model-based 방식으로 대체하는 hybrid 전략
- **CMOS 이미지 센서**: SKOPC의 비표준 레이어(CIS 픽셀) 지원 시 serif 보정 기능 참고
- **Serif 구현**: 45도 retargeting 기법은 구현이 단순하며 기존 OPC 엔진과 호환성 높음

## 태그
`Recipe`, `SPIE`, `Corner Rounding`, `Serif`, `Model-Based OPC`, `CMOS Image Sensor`, `CIS`, `Retargeting`, `Photomask`
