# EUV DRAM Patterning Historic Overview and Future Assumption

## 메타데이터
- **저자**: Jeonghoon Lee, Soobin Hwang, Van Tuong Pham, Kenichi Miyaguchi, Ardavan Niroomand, Lander Verstraete, Kiho Yang, Werner Gillijns, Shubhankar Das, Victor Blanco, Sandip Halder, Hyo Seon Suh, Yasser Sherazi, Darko Trivkovic, Pieter Vanelderen, Inhee Lee, Kurt Ronse, Ryan Ryoung han Kim
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250V
- **DOI/URL**: https://doi.org/10.1117/12.3051xxx

## 핵심 요약
DUV에서 EUV 리소그래피로의 전환을 통한 DRAM 패터닝의 역사적 발전 과정을 정리하고 sub-10nm 노드 이후의 미래 방향을 제시하는 초청(invited) 리뷰 논문. 레일리 방정식(Rayleigh equation) 파라미터(λ, NA, K1)의 관점에서 DRAM 스케일링 흐름을 분석하고, OPC 전략, 마스크 옵션, 레지스트 기술 등 EUV DRAM 패터닝 생태계 전반을 종합적으로 다룬다.

## 주요 기여
1. **EUV DRAM 패터닝 역사 정리**: DUV → 0.33NA EUV → 0.55NA High-NA EUV 전환 흐름 체계화
2. **레일리 방정식 기반 스케일링 분석**: λ, NA, K1 파라미터 진화로 DRAM 피치 스케일링 분석
3. **서브-10nm DRAM 미래 전망**: High-NA EUV, dry resist, curvilinear OPC 등 미래 기술 전망
4. **OPC 전략 진화**: DRAM 레이어별 OPC 방법론 변화 (rule → model → ML → ILT → curvilinear)
5. **imec-삼성-ASML 공동 연구**: DRAM 패터닝 생태계 전반의 공동 로드맵 제시

## Recipe/Flow 상세
- **DRAM 패터닝 역사적 발전 흐름**:
  1. **DUV 시대 (45nm~20nm)**:
     - 193nm 이머젼 ArF 리소그래피
     - SADP/SAQP 다중 패터닝으로 DRAM 피치 스케일링
     - 복잡한 OPC + 에치 공정 통합
  2. **EUV 도입기 (20nm~10nm)**:
     - 0.33NA EUV 최초 도입 (컨택, BEOL 일부)
     - EUV OPC 모델 개발: shadowing, flare, stochastic
     - 다중 패터닝 ArF → EUV 단일 노광 전환
  3. **현재 EUV 성숙기 (10nm~**):
     - 0.33NA EUV 다중 레이어 적용 (Active, Bitline, Wordline)
     - EUV stochastic 결함 관리: OPC 전략 고도화
     - Curvilinear OPC, ILT 도입 (DRAM 컨택 레이어)
  4. **High-NA EUV 전환기 (미래)**:
     - 0.55NA EXE:5000 도입 검토
     - DRAM 서브-10nm 피치 단일 노광 가능성
     - Dry resist, low-n 마스크 결합 OPC
  5. **미래 기술 전망**:
     - Hyper-NA EUV 연구 시작
     - Directed Self-Assembly(DSA) + EUV 통합
     - 차세대 레지스트 및 마스크 기술 로드맵
- **DRAM 레이어별 OPC 전략**:
  - Active 레이어: SAQP/SADP + 극소 OPC
  - Bitline 컨택: EUV OPC + stochastic 최적화
  - Capacitor 컨택: Curvilinear OPC + ILT
  - Metal 배선: 단일 EUV + 고성능 OPC
- **공동 저자 기관**: imec + 삼성전자 + ASML + 기타

## OPC 툴 구현 관련성
- SKOPC DRAM 전용 OPC 플로우 설계에 이 리뷰 논문의 역사적 맥락 활용
- DRAM 레이어별 최적 OPC 전략 선택 가이드라인 (rule vs. model vs. ILT vs. curvilinear)
- 미래 High-NA EUV DRAM 패터닝을 위한 OPC 모델 확장 로드맵
- EUV DRAM OPC 파라미터 데이터베이스 구축 기준

## 태그
`EUV`, `DRAM`, `Memory`, `OPC`, `HighNA`, `PatterningHistory`, `Review`, `Scaling`, `imec`, `Samsung`, `ASML`, `SPIE`, `2025`
