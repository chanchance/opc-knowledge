# Improved Line-End Foreshortening and Corner-Rounding Control in Optical Proximity Correction Using Radius of Curvature Method

## 메타데이터
- **저자**: Maharaj Mukherjee, Vinhthuy Phan
- **소속**: IBM Microelectronics, SUNY/Stony Brook
- **연도**: 2002
- **게재지**: Proc. SPIE 4691, Optical Microlithography XV
- **DOI/URL**: https://doi.org/10.1117/12.474487

## 핵심 요약
OPC에서 line-end foreshortening(라인 끝 단축)과 corner rounding(코너 라운딩)을 개선된 방식으로 제어하는 곡률 반경(radius of curvature) 방법을 제안한다. 전통적인 직사각형 serif와 anchor 대신 rounded(곡선형) serif와 anchor를 사용하여 더 작은 크기로도 효과적인 보정을 달성하며, 마스크 규칙 제약(mask rule constraint)을 더 쉽게 충족한다.

## 주요 기여
1. **곡률 반경 기반 serif 설계**: 직사각형 대신 곡선형 serif/anchor → 동일 보정 효과를 더 작은 크기로 달성
2. **MRC 충족 용이성**: 작은 rounded serif가 rectilinear serif보다 마스크 규칙 충족에 유리
3. **Line-end foreshortening 제어**: 라인 끝 단축 현상을 hammer-head 대신 곡선형 보정 구조로 제어
4. **Corner rounding 제어**: 코너 라운딩 보정을 곡률 반경 파라미터로 정량적으로 설계
5. **OPC 통합**: 곡률 반경 방법을 기존 model-based OPC 루프에 통합하는 방법론

## Recipe/Flow 상세
```
[Radius of Curvature OPC Flow]
1. Line-end 및 corner 위치 식별:
   - 레이아웃에서 line-end (볼록 끝단) 추출
   - 볼록/오목 코너 위치 분류
2. 곡률 반경 파라미터 결정:
   - 패턴 크기 및 공정 조건에 따른 최적 serif 곡률 반경 설정
   - Rule-based 룩업 테이블 또는 model-based 최적화
3. Rounded Serif/Anchor 생성:
   - Line-end: rounded hammer-head serif 추가 (곡선 끝 처리)
   - Corner: rounded corner serif 추가 (곡률 반경 적용)
   - 크기: 전통 rectilinear serif보다 소형화 가능
4. Model-Based OPC 실행:
   - rounded serif 포함 타겟으로 OPC 실행
   - EPE 계산 및 수렴
5. MRC 검증:
   - rounded serif 크기 MRC 충족 확인
   - 전통 serif 대비 MRC 위반 건수 비교
```

### 핵심 파라미터
- **곡률 반경**: serif 끝단의 곡률 (작을수록 더 둥근 형상)
- **Serif 유형**: rounded anchor (line-end), rounded serif (corner)
- **크기 이점**: rectilinear 대비 소형화로 MRC 충족 용이
- **적용 대상**: line-end foreshortening, 볼록 코너 라운딩

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: line-end 및 corner 보정 단계에 곡률 반경 기반 serif 생성 통합 참고
- `skopc/modeling/rule_opc.py`: rule-based OPC에서 line-end hammer-head 및 corner serif 규칙 설계 참고
- **Serif 구현**: SKOPC의 OPC 보정 형상 라이브러리에 rounded serif 유형 추가 시 이 논문의 곡률 파라미터 활용
- **MRC 최적화**: 작은 rounded serif로 마스크 규칙 위반을 최소화하는 serif 설계 전략

## 태그
`Recipe`, `SPIE`, `Line-End Shortening`, `Corner Rounding`, `Serif`, `Anchor`, `Radius of Curvature`, `OPC`, `Hammer-Head`, `MRC`, `2002`
