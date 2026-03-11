# Curvilinear Mask Process Correction - Status Quo and Outlook

## 메타데이터
- **저자**: Ingo Bork, Kushlendra Mishra, Rachit Sharma, Mary Zuo (Siemens EDA / Mentor)
- **연도**: 2022
- **게재지**: IEEE SEMI Advanced Semiconductor Manufacturing Conference (ASMC) 2022
- **DOI/URL**: https://ieeexplore.ieee.org/document/9972290/

## 핵심 요약
Multi-Beam Mask Writer(MBMW) 보급 확대와 웨이퍼 리소그래피 이점에 따라 curvilinear 마스크 형상의 효율적인 처리가 점점 중요해지고 있다. 본 논문은 curvilinear Mask Process Correction(CLMPC)의 현황을 정리하고, post tape-out 플로우에서 curvilinear 형상 처리의 전망을 제시한다. MRC 요구사항, 마스크 검사 영향, 파일 크기 압축 접근법, 네이티브 커브 포맷 기반 새로운 데이터 표현 방법을 다룬다.

## 주요 기여
1. **CLMPC 현황 정리**: 2022년 기준 curvilinear MPC 기술의 성숙도 및 한계 종합
2. **MRC 요구사항 분석**: incoming curvilinear 데이터에 대한 Mask Rule Check 기준 정립
3. **마스크 검사 영향**: curvilinear 패턴이 마스크 검사 공정에 미치는 영향 분석
4. **파일 크기 압축**: curvilinear 형상의 대용량 데이터 처리를 위한 압축 방법론
5. **네이티브 커브 포맷**: 다각형 근사 대신 베지어/스플라인 기반 네이티브 곡선 표현

## Recipe/Flow 상세
- **Curvilinear MPC 플로우**:
  1. ILT/curvilinear OPC 결과물 수신 (polygonal 또는 native curve 포맷)
  2. MRC(Mask Rule Check): width, space, area, curvature 검사
  3. CLMPC 적용: 마스크 제조 공정의 e-beam proximity 보정
  4. 검사 friendliness 최적화
  5. 데이터 압축 및 MBMW 포맷 변환
- **MRC 항목**:
  - 최소 선폭/간격 (CD constraints)
  - 최소 곡률 반경
  - 패턴 면적 제한
- **MBMW 연계**: Multi-Beam Mask Writer의 Pixel Level Dose Correction(PLDC)와 CLMPC 통합

## OPC 툴 구현 관련성
- Curvilinear OPC 결과물의 MRC 검사 항목 구현 기준
- CLMPC 단계를 OPC 플로우 후단에 추가하는 방법
- 베지어 기반 데이터 표현 → 파일 크기 최적화
- `mask_rule_check.py` curvilinear 확장 시 curvature constraint 추가 참고

## 태그
`CurvilinearMask`, `MPC`, `MRC`, `MBMW`, `OPC`, `Manufacturing`, `IEEE`, `2022`
