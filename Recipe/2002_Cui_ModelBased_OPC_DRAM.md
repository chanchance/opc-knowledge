# Is Model-Based Optical Proximity Correction Ready for Manufacturing? Study on 0.12- and 0.175-µm DRAM Technology

## 메타데이터
- **저자**: Yuping Cui, Franz X. Zach, Shahid A. Butt, Wai-Kin Li, Bernhard Liegl, Lars W. Liebmann
- **소속**: IBM Microelectronics, Infineon Technologies Corp.
- **연도**: 2002
- **게재지**: Proc. SPIE 4691, Optical Microlithography XV
- **DOI/URL**: https://doi.org/10.1117/12.474618

## 핵심 요약
0.12µm 및 0.175µm DRAM 기술 노드에서 전통적인 rule-based OPC와 model-based OPC를 비교하여, model-based OPC의 양산 적용 준비 상태를 평가한다. ArF 및 KrF 리소그래피, off-axis illumination(OAI), 위상 편이 마스크(PSM)를 사용한 full-chip 실험을 통해 두 방식의 1D 및 2D 구조에서의 성능 차이를 정량적으로 분석한다.

## 주요 기여
1. **Rule-based vs. Model-based OPC 비교**: DRAM 실제 레이아웃에서 두 방식의 line width 제어 및 line-end 인쇄 정밀도 비교
2. **1D/2D 구조 성능 분석**: 1D 구조(라인/공간)에서는 두 방식 모두 유사 성능, 2D 구조(line-end 등)에서는 model-based가 우세
3. **공정 윈도우 한계 발견**: model-based OPC 결과에서도 일부 레이아웃 패턴에서 심각한 공정 윈도우 제한 발생 — 원인 분석 제공
4. **DRAM 적용 가이드라인**: ArF/KrF 리소그래피에서 OAI + PSM 조합별 OPC 전략 비교
5. **양산 준비 평가**: model-based OPC가 DRAM 양산에 적용 가능한 수준인지 정량적으로 평가한 초기 연구

## Recipe/Flow 상세
```
[DRAM Model-Based OPC 비교 실험 Flow]
1. 테스트 레이아웃 준비:
   - 0.12µm DRAM: ArF (193nm) 리소그래피
   - 0.175µm DRAM: KrF (248nm) 리소그래피
   - Off-axis illumination (OAI) + PSM 적용
2. Rule-Based OPC:
   - 1D 비교 테이블 기반 edge bias 적용
   - 2D 보정 규칙 (line-end hammer-head 등)
3. Model-Based OPC:
   - 광학 모델 + resist 모델 calibration
   - Edge segment 이동 기반 반복 최적화
4. 비교 평가:
   - 1D 구조: line width uniformity 측정
   - 2D 구조: line-end shortening, corner rounding 측정
   - Process window: DOF-EL (Depth of Focus - Exposure Latitude) 다이어그램
5. 공정 윈도우 제한 원인 분석:
   - model-based OPC 실패 패턴 유형 분류
   - 개선 방향 제시
```

### 핵심 파라미터
- **기술 노드**: 0.12µm (ArF) / 0.175µm (KrF) DRAM
- **조명**: Off-axis illumination (OAI)
- **마스크**: Phase Shift Mask (PSM)
- **비교 지표**: line width 제어 정확도, line-end 인쇄 품질, 공정 윈도우(DOF × EL)

## OPC 툴 구현 관련성
- `skopc/modeling/rule_opc.py` vs `skopc/modeling/model_opc.py`: 두 방식의 성능 차이에 대한 이론적 근거 제공
- **DRAM contact 레이어**: SKOPC의 contact/via 레이어 OPC 전략 수립 시 이 논문의 실험 결과 참고
- **공정 윈도우 분석**: `skopc/pwo/`의 PWO와 연계하여 OPC 후 공정 윈도우 한계 분석 방법 참고
- **Rule-based 한계**: rule-based OPC가 충분하지 않은 패턴 유형 식별 — model-based 전환 기준 설정에 활용
- `recipes/example_arfimm.yaml`: ArF DRAM OPC recipe 파라미터 설정의 역사적 기준점

## 태그
`Recipe`, `SPIE`, `Model-Based OPC`, `Rule-Based OPC`, `DRAM`, `ArF`, `KrF`, `OAI`, `PSM`, `Process Window`, `Line-End Shortening`, `양산 적용`
