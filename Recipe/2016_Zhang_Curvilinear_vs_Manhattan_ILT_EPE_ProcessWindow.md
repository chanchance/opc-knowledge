# Comparing Curvilinear vs Manhattan ILT Shape Efficacy on EPE and Process Window

## 메타데이터
- **저자**: Dan Zhang, Peter Buck, Alexander Tritchkov, Saikiran Madhusudhan, James Word
- **소속**: (Mentor Graphics 등)
- **연도**: 2016
- **게재지**: Proc. SPIE 9985, Photomask Technology 2016, 99850V
- **DOI/URL**: https://doi.org/10.1117/12.2243030

## 핵심 요약
ILT(Inverse Lithography Technology)가 생성하는 곡선형(curvilinear) 마스크 출력과 이를 Manhattan(직사각형) 형상으로 근사화(Manhattanize)한 출력을 웨이퍼 레벨 리소그래피 시뮬레이션으로 비교한다. 당시 최첨단 노드와 MRC 규칙에서 raw curvilinear ILT vs. Manhattanized ILT의 EPE 및 공정 윈도우 차이를 정량적으로 분석한 선구적 연구다.

## 주요 기여
1. **Curvilinear vs. Manhattan 정량 비교**: 동일 ILT 최적화 결과를 Manhattan 근사화 전후로 비교 → EPE, 공정 윈도우 차이 정량화
2. **Manhattanization 손실 분석**: 곡선형 ILT를 직사각형으로 변환할 때 발생하는 성능 저하 규명
3. **ILT repair 전략 검증**: conventional OPC로 부족한 공정 윈도우를 ILT로 국소 보완하는 접근법의 curvilinear 효과 확인
4. **MRC 제약 하의 비교**: 당시 MRC(Mask Rule Check) 규칙 하에서 달성 가능한 curvilinear 이점 평가
5. **선진 노드 대상**: 당시 최첨단 노드 레이아웃에서의 현실적 비교

## Recipe/Flow 상세
```
[Curvilinear vs. Manhattan ILT 비교 실험 Flow]
1. ILT 최적화 실행:
   - 동일 레이아웃에 대해 pixel/level-set 기반 ILT 실행
   - 출력: raw curvilinear 마스크 (픽셀 값 또는 연속 경계)
2. Manhattan 근사화 (Manhattanization):
   - Curvilinear ILT 출력을 직사각형 폴리곤으로 변환
   - MRC 준수하는 수준으로 근사화 (당시 MRC 기준)
3. 웨이퍼 시뮬레이션 비교:
   - Curvilinear mask → 리소그래피 시뮬레이션 → EPE, 공정 윈도우
   - Manhattan mask → 리소그래피 시뮬레이션 → EPE, 공정 윈도우
4. 결과 비교 분석:
   - EPE 개선량: curvilinear vs. Manhattan
   - 공정 윈도우(DOF-EL): curvilinear vs. Manhattan
   - Manhattanization으로 인한 성능 손실 정량화
5. 결론: curvilinear 마스크의 추가적 이점 확인
```

### 핵심 파라미터
- **비교 대상**: raw curvilinear ILT 출력 vs. Manhattanized ILT 출력
- **평가 지표**: EPE, 공정 윈도우 (DOF × EL)
- **MRC**: 당시 첨단 노드 Mask Rule Check 기준 적용
- **시뮬레이션**: 웨이퍼 레벨 리소그래피 시뮬레이션

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: curvilinear OPC 도입 여부 결정 시 이 논문의 정량적 이점 근거로 활용
- **Manhattanization 비용**: SKOPC에서 ILT 결과를 Manhattan으로 변환할 때 발생하는 성능 손실 예측 참고
- **Curvilinear 정당화**: EUV 노드에서 curvilinear 마스크 지원을 SKOPC에 추가하는 로드맵의 근거 자료
- `recipes/example_euv.yaml`: EUV 레시피에서 `mask_type: curvilinear` vs `manhattan` 선택 기준 참고

## 태그
`Recipe`, `SPIE`, `Curvilinear Mask`, `Manhattan`, `ILT`, `EPE`, `Process Window`, `Manhattanization`, `MRC`, `2016`, `Photomask Technology`
