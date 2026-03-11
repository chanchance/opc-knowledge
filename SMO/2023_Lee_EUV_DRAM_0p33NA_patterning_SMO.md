# Patterning Assessment Using 0.33NA EUV Single Mask for Next Generation DRAM Manufacturing

## 메타데이터
- **저자**: Jeonghoon Lee, Sandip Halder, Van Tuong Pham, Roberto Fallica, Seonggil Heo, Kaushik Sah, Hyo Seon Suh, Victor Blanco, Werner Gillijns, Andrew Cross, Ethan Maguire, Ana-Maria Armeanu, Vladislav Liubich, Evgeny Malankin, Xima Zhang, Monica Kempsell Sears, Neal Lafferty, Germain Fenger, Chih-I Wei, Ryoung Han Kim
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950S (28 April 2023)
- **DOI/URL**: https://doi.org/10.1117/12.2660763

## 핵심 요약
0.33NA EUV 단일 마스크를 사용하여 차세대 DRAM의 핵심 레이어(Bit-Line Periphery, Storage Node Landing Pad)를 sub-40nm 피치로 패터닝하는 타당성을 연구한다. SMO와 공중이미지 기반 OPC를 결합하여 잠재적 취약점을 사전 식별하고, 웨이퍼 실험을 통해 검증한다.

## 주요 기여
1. **DRAM 핵심 레이어 SMO 적용**: BLP(Bit-Line Periphery)와 SNLP(Storage Node Landing Pad) 레이어에 SMO+OPC 플로우 적용
2. **공정 마진 분석**: KLA 검사를 통한 체계적 결함률 및 공정 마진 분석
3. **이중 마스크 전략 제안**: 리타겟 바이어스 스플릿 및 레지스트 모델 OPC를 사용하는 보조 마스크로 도즈 약 30% 감소
4. **레지스트 타입 비교**: 다양한 포토레지스트 타입의 EUV 단일 패터닝 성능 비교

## 알고리즘/수식
### SMO + OPC 플로우
```
단계 1: SMO 수행
  - 소스: 0.33NA EUV 스캐너용 조명 최적화
  - 마스크: DRAM BLP/SNLP 레이어 패턴 최적화
  - 출력: 최적 소스 형상 + OPC 마스크 패턴

단계 2: 공중이미지 기반 OPC
  - 공중이미지 시뮬레이션으로 약점 패턴 식별
  - 모델 기반 OPC로 마스크 바이어스 보정
  - SRAF 최적 배치

단계 3: 공정 창 검증 (PWD 웨이퍼)
  - KLA 검사로 체계적 패터닝 결함 분석
  - 포커스-도즈 행렬 분석
```

### 성능 지표
- 피치: sub-40nm (BLP/SNLP 레이어)
- 노드: 10nm DRAM
- 이중 마스크 전략으로 도즈 ~30% 감소
- NA: 0.33 (표준 EUV)

## OPC 툴 SMO 구현 관련성
- DRAM 메모리 레이어의 SMO 적용 사례 — 로직 외 메모리 타겟에 대한 SMO 플로우 참조
- 공정 창 검색(PWD) 웨이퍼 실험과 SMO 결과 연계 방법론
- 이중 마스크 전략: SMO 결과 기반 마스크 분할 전략 수립에 활용
- sub-40nm 피치에서 단일 EUV 패터닝 한계와 SMO 역할 정량화

## 태그
`SMO`, `OPC`, `EUV`, `DRAM`, `0.33NA`, `single_patterning`, `BLP`, `SNLP`, `process_window`, `SPIE`
