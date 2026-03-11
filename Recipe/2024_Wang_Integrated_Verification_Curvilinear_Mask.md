# An Integrated Verification Flow for Curvilinear Mask

## 메타데이터
- **저자**: Shuling Wang, Shumay Shang, Sagar Saxena, Xima Zhang, George Lippincott, Le Hong, John L. Sturtevant
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295415
- **DOI/URL**: https://doi.org/10.1117/12.3010925

## 핵심 요약
Curvilinear 마스크는 맨해튼(Manhattan) 마스크 대비 향상된 공정 창, PV 밴드, MEEF 등의 리소그래피 성능을 보이나, 복잡한 마스크 형상, 대용량 데이터, 마스크 룰 체크(MRC) 등 고유한 검증 과제가 있다. 본 논문은 OPC/ILT로 생성된 curvilinear 마스크 데이터에 대한 통합 검증 플로우를 제시하며, MRC 규칙 설계, 형상 검증, 웨이퍼 프린터빌리티 확인을 포괄하는 end-to-end 검증 방법론을 개발한다.

## 주요 기여
1. **Curvilinear 마스크 통합 검증 플로우**: OPC 후 curvilinear 데이터의 MRC, 형상 검증, 프린터빌리티 확인 통합
2. **Curvilinear MRC 규칙 설계**: 기존 Manhattan MRC와 다른 곡선 형상 전용 MRC 규칙 체계
3. **대용량 Curvilinear 데이터 처리**: 복잡한 곡선 형상의 효율적인 검증 알고리즘
4. **OPC 품질 보증**: Curvilinear OPC/ILT 결과의 마스크 제조성 및 웨이퍼 성능 검증
5. **Siemens EDA Calibre 통합**: Calibre 플랫폼에서 curvilinear 마스크 검증 워크플로우

## Recipe/Flow 상세
- **Curvilinear 마스크 통합 검증 플로우**:
  1. **Curvilinear 데이터 입력**:
     - OPC(곡선형 OPC) 또는 ILT 출력 curvilinear 마스크 데이터
     - MULTIGON 또는 베지어 곡선 형식 데이터
     - EUV 또는 ArF 마스크 타겟
  2. **Curvilinear MRC (마스크 룰 체크)**:
     - 곡선 반경 최소값 확인
     - 곡선 세그먼트 최소 길이
     - 인접 패턴 간 최소 간격
     - 마스크 기록 장비(e-beam, MBMW) 한계 기반 규칙
  3. **형상 검증**:
     - 의도한 설계와 OPC 결과 형상 비교
     - 날카로운 돌출(spike), 고리(loop) 등 비정상 형상 검출
     - 데이터 연속성 및 토폴로지 검사
  4. **웨이퍼 프린터빌리티 검증**:
     - Curvilinear 마스크 시뮬레이션: EPE, CD 균일도 확인
     - 공정 창(DOF/EL) 시뮬레이션
     - 핫스팟 스크리닝: MRC 위반 패턴의 웨이퍼 영향 평가
  5. **피드백 루프**:
     - 검증 실패 패턴 → OPC 파라미터 수정
     - MRC 위반 자동 수정 옵션
     - 검증 통과 후 마스크 제조 승인
- **Curvilinear 검증의 주요 과제**:
  - 데이터 볼륨: 곡선 형상은 Manhattan 대비 수배 큰 데이터
  - MRC 복잡성: 직선 기반 MRC와 근본적으로 다른 규칙 체계
  - 검증 런타임: 대용량 데이터의 full-chip 검증 속도
- **소속 기관**: Siemens EDA (미국)

## OPC 툴 구현 관련성
- SKOPC curvilinear OPC/ILT 출력에 통합 검증 플로우 추가
- `curvilinear_verification.py`: MRC, 형상 검증, 프린터빌리티 확인 통합 모듈
- Curvilinear MRC 규칙 라이브러리: 반경, 간격, 세그먼트 길이 규칙
- 검증 실패 자동 피드백 → OPC 파라미터 수정 루프

## 태그
`CurvilinearMask`, `Verification`, `MRC`, `OPC`, `ILT`, `MaskRuleCheck`, `Printability`, `FullChip`, `Siemens`, `Calibre`, `SPIE`, `2024`
