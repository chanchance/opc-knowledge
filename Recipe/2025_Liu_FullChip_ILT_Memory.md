# Exploration of Imaging Performance for Full Chip ILT in Memory Product

## 메타데이터
- **저자**: Xiaonan Liu, Futian Wang, Juan Wei, Ruihua Liu, Fu Li, Chong Wang, Jiangliu Shi, Qingchen Cao
- **소속**: (SPIE Advanced Lithography + Patterning 2025 게재)
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 134241A
- **DOI/URL**: https://doi.org/10.1117/12.3051597

## 핵심 요약
메모리(Memory) 제품의 전체 칩(full chip) 규모에서 ILT(Inverse Lithography Technology)의 이미징 성능을 탐구한다. 메모리 제품 특유의 고밀도 반복 패턴(DRAM 셀, NAND 플래시 등)에서 full chip ILT 적용 시 이미징 품질, 런타임, 마스크 복잡도 간의 트레이드오프를 분석하고 실용적 full chip ILT 플로우를 제시한다.

## 주요 기여
1. **메모리 제품 full chip ILT**: DRAM/NAND 등 메모리 레이아웃 특성(고밀도 반복 셀)에 최적화된 ILT 적용 전략
2. **이미징 성능 분석**: full chip ILT의 EPE, MEEF, 공정 윈도우 등 핵심 지표 정량적 평가
3. **런타임 vs. 품질 트레이드오프**: full chip 규모에서 ILT 정확도와 계산 시간 간 균형 전략
4. **마스크 복잡도 관리**: ILT 생성 curvilinear 마스크의 데이터 볼륨 및 MPC 부담 분석
5. **실용적 플로우**: 산업 메모리 tape-out에 적용 가능한 full chip ILT 파이프라인 제시

## Recipe/Flow 상세
```
[Full Chip ILT for Memory Product Flow]
1. 메모리 레이아웃 분석:
   - 셀 어레이(반복 패턴) vs. 주변 회로(임의 패턴) 분리
   - 임계 레이어(critical layer) 식별
2. 레이어별 ILT 전략 결정:
   - 셀 어레이: 대표 셀 ILT 최적화 후 타일링(tiling) 적용
   - 주변 회로: 개별 패턴별 ILT 최적화
3. ILT 최적화 실행:
   - 광학 모델 (Hopkins/TCC 기반)
   - Pixel-based 또는 level-set ILT
   - 수렴 기준: EPE < target
4. Full Chip 통합:
   - 셀 타일 + 주변 회로 ILT 결과 합성
   - 경계 영역(boundary) 처리
5. 성능 검증:
   - Imaging 품질: EPE, CD uniformity, MEEF
   - 공정 윈도우 (DOF-EL 다이어그램)
   - 마스크 복잡도 및 MPC 부담 평가
6. 마스크 제조 플로우 (MPC, fracture, writing)
```

### 핵심 파라미터
- **적용 제품**: 메모리 (DRAM/NAND) critical layer
- **ILT 유형**: full chip (셀 타일링 + 주변 회로 개별 처리)
- **평가 지표**: EPE, CD uniformity, 공정 윈도우, 마스크 복잡도
- **발표 연도**: 2025 (SPIE Advanced Lithography + Patterning, San Jose)

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: 메모리 제품 레이아웃에서 ILT와 OPC 혼합 전략 참고
- **메모리 레이아웃 최적화**: SKOPC에서 반복 셀 패턴 처리 시 타일링 기반 ILT 효율화 구현 참고
- `skopc/pwo/`: 메모리 critical layer의 공정 윈도우 최적화와 ILT 연계 참고
- `recipes/example_euv.yaml`: EUV 메모리 노드에서 ILT 기반 레시피 파라미터 설계 기준

## 태그
`Recipe`, `SPIE`, `ILT`, `Full Chip`, `Memory`, `DRAM`, `NAND`, `Curvilinear Mask`, `2025`, `SPIE Advanced Lithography`
