# Exploration of Imaging Performance for Full Chip ILT in Memory Product

## 메타데이터
- **저자**: Xiaonan Liu, Futian Wang, Juan Wei, Ruihua Liu, Fu Li, Chong Wang, Jiangliu Shi, Qingchen Cao
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 134241A
- **DOI/URL**: https://doi.org/10.1117/12.3051597

## 핵심 요약
메모리 제품의 어레이 패턴에 full-chip ILT(Inverse Lithography Technology)를 적용하여 기존 OPC 대비 리소그래피 성능 향상을 분석한다. 다양한 피치와 엇갈린 어레이 구성의 4가지 패턴 설계를 선정하여 NILS, MEEF, PVB, DOF 지표를 체계적으로 비교하고, ILT가 밀집 및 엇갈린 어레이 패턴에서 우수한 성능을 보임을 실증한다.

## 주요 기여
1. **메모리 어레이 Full-chip ILT**: 메모리 제품 특화 어레이 패턴에서 full-chip ILT 구현
2. **NILS 및 DOF 향상**: ILT가 기존 OPC 대비 NILS와 DOF에서 우수한 성능 달성
3. **다양한 피치 패턴 비교**: 밀집 및 엇갈린 어레이 구성에서 ILT vs. OPC 체계적 비교
4. **4가지 지표 기반 평가**: NILS, MEEF, PVB, DOF를 종합하여 ILT 장점 정량화
5. **메모리 OPC 프레임워크 통합**: 기존 메모리 OPC 워크플로우 내 ILT 통합 경로 제시

## Recipe/Flow 상세
- **메모리 Full-chip ILT 평가 플로우**:
  1. **테스트 패턴 선정**:
     - 4가지 패턴 설계: 서로 다른 피치, 밀집(dense) vs. 엇갈린(staggered) 어레이
     - 메모리 DRAM/NAND 특유의 규칙적 어레이 구조
     - 피치 범위: 메모리 제품 실제 설계 규칙 기반
  2. **OPC 기준선 생성**:
     - 기존 모델 기반 OPC로 마스크 보정
     - NILS, MEEF, PVB, DOF 기준값 측정
  3. **Full-chip ILT 적용**:
     - 동일 패턴에 ILT 기반 마스크 최적화
     - 비용 함수: EPE 최소화 + 공정 창 최대화
     - MRC 준수 곡선형(curvilinear) 마스크 생성
  4. **성능 비교**:
     - NILS: 이미지 로그 기울기 (선명도 지표)
     - MEEF: 마스크 오차 증폭 계수
     - PVB: 공정 변동 밴드 (공정 창 지표)
     - DOF: 초점 심도
  5. **결과 분석**:
     - 밀집 어레이: ILT의 NILS, DOF 향상 두드러짐
     - 엇갈린 어레이: PVB 감소로 공정 창 개선
     - MEEF는 패턴 유형에 따라 결과 다름
- **메모리 어레이 ILT 특수 고려사항**:
  - 매우 규칙적인 패턴 → ILT 비용 함수 단순화 가능
  - 대규모 반복 패턴 → GPU 병렬 처리로 런타임 최적화
  - 마스크 복잡도 관리: curvilinear vs. rectilinear 마스크 선택
- **소속 기관**: Beijing Superstring Academy of Memory Technology (중국)

## OPC 툴 구현 관련성
- SKOPC 메모리 레이어 OPC에서 ILT 옵션 추가
- `memory_ilt.py`: 어레이 패턴 특화 ILT 최적화 (규칙적 반복 구조 활용)
- NILS/MEEF/PVB/DOF 기반 ILT vs. OPC 자동 선택 로직
- Full-chip ILT 런타임 관리: 패턴 반복성을 이용한 GPU 병렬화

## 태그
`ILT`, `InverseLithography`, `FullChip`, `Memory`, `DRAM`, `NAND`, `OPC`, `NILS`, `DOF`, `ProcessWindow`, `SPIE`, `2025`
