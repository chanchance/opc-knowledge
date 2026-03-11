# SRAF Insertion for VIA-like Layers Using laSRAF Method

## 메타데이터
- **저자**: Andrey Lutich
- **소속**: (32nd European Mask and Lithography Conference 게재)
- **연도**: 2016
- **게재지**: Proc. SPIE 10032, 32nd European Mask and Lithography Conference, 100320K
- **DOI/URL**: https://doi.org/10.1117/12.2248015

## 핵심 요약
VIA 레이어와 같은 2D 패턴에 대한 SRAF 삽입을 위해 laSRAF(Linearly Added SRAF) 방법을 제안한다. 사전 계산된 SRAF 유용성(usefulness) 템플릿의 선형 중첩(linear superposition)에 기반하여 복잡한 2D 레이아웃에서도 빠르고 정확하게 SRAF를 배치한다. 두 단계로 구성: (i) 임의 레이아웃에 대한 SRAF usefulness map 생성, (ii) MRC(Mask Rule Check)를 준수하는 SRAF 형상 도출.

## 주요 기여
1. **laSRAF (선형 중첩 SRAF)**: 사전 계산된 SRAF usefulness 템플릿을 선형으로 더해 복잡한 레이아웃의 SRAF usefulness map 빠르게 생성
2. **VIA 레이어 특화**: 2D 패턴(contact hole, via) 특성에 최적화된 SRAF 삽입 전략
3. **MRC 준수 SRAF 도출**: usefulness map에서 마스크 규칙 검사를 충족하는 실제 SRAF 형상 자동 산출
4. **계산 효율성**: ILT 대비 훨씬 빠른 속도로 고품질 SRAF 삽입 — full-chip 적용 가능
5. **공정 윈도우 최적화**: overlapped process window 최대화를 목표로 하는 usefulness 정의

## Recipe/Flow 상세
```
[laSRAF Flow]
1. 템플릿 사전 계산 (오프라인):
   - 단순 패턴 유형별 SRAF usefulness 템플릿 계산
   - 광학 파라미터 (NA, sigma, wavelength) 기반
2. SRAF Usefulness Map 생성 (온라인):
   - 실제 레이아웃 패턴에 usefulness 템플릿 선형 중첩
   - 각 위치에서 SRAF를 배치할 때의 공정 윈도우 개선 효과 맵화
3. MRC 준수 SRAF 형상 도출:
   - Usefulness map에서 양수(beneficial) 영역 추출
   - MRC(최소 선폭, 최소 간격) 적용하여 실제 SRAF 형상으로 변환
4. OPC와의 통합:
   - 생성된 SRAF를 main feature OPC와 함께 처리
   - SRAF 인쇄(printing) 위험 검증
```

### 핵심 파라미터
- **방법**: 선형 중첩 (linear superposition) of usefulness templates
- **적용 레이어**: VIA-like 2D 패턴 (contact hole, via array)
- **MRC 준수**: 최소 선폭, 최소 간격 마스크 규칙 자동 적용
- **목표**: overlapped process window 최대화

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: SRAF 삽입 기능에 laSRAF 방법 통합 참고
- **VIA/Contact 레이어**: SKOPC에서 VIA 및 contact hole 레이어의 SRAF 삽입 구현 시 직접 참고
- **계산 효율**: ILT 대신 템플릿 중첩 방식으로 빠른 SRAF 생성 가능 — full-chip 처리에 유리
- `recipes/example_arfimm.yaml`: VIA 레이어 SRAF 파라미터 (`sraf_insertion_method: laSRAF`) 설정 참고

## 태그
`Recipe`, `SPIE`, `SRAF`, `VIA`, `Contact Hole`, `laSRAF`, `Linear Superposition`, `MRC`, `Process Window`, `Full-Chip`
