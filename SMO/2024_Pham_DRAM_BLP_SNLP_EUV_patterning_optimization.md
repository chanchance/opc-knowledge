# Patterning Optimization for Single Mask Bit-Line-Periphery and Storage-Node-Landing-Pad DRAM Layers Using 0.33NA EUV Lithography at the Resolution Limit

## 메타데이터
- **저자**: Van Tuong Pham, Jeonghoon Lee, Kaushik Sah, Ying-Lin Chen, Seonggil Heo, Soobin Hwang, Kenichi Miyaguchi, Bappaditya Dey, Maria Chistiakova, Peter De Schepper, Philippe Bezard, Sara Paolillo, Danilo De Simone, Hyo Seon Suh, Victor Blanco
- **소속**: imec, KLA Corp., Inpria Corp. (벨기에)
- **연도**: 2024
- **게재지**: Proc. SPIE 12957, Advances in Patterning Materials and Processes XLI, 129570V (9 April 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010934

## 핵심 요약
0.33NA EUV 리소그래피를 사용하여 차세대 DRAM의 BLP(Bit-Line Periphery) 및 SNLP(Storage Node Landing Pad) 레이어를 단일 마스크로 패터닝하는 최적화 연구. 해상도 한계에서의 공정 개발을 통해 DOF 119nm, EL 25% (도즈-to-size 89.4mJ/cm²)의 대면적 공정 창을 달성한다.

## 주요 기여
1. **단일 마스크 DRAM 솔루션 개발**: BLP 및 SNLP 레이어의 단일 EUV 마스크 공정 최적화
2. **해상도 한계 공정 창 달성**: DOF 119nm, EL 25%의 무결함 공정 창 확보
3. **다중 레지스트 비교**: 유기 및 금속 산화물 레지스트 성능 비교
4. **imec 실험적 검증**: 실제 웨이퍼 제작 및 KLA 검사를 통한 결과 검증

## 알고리즘/수식
### SMO + OPC 최적화 플로우
```
단계 1: SMO (소스-마스크 최적화)
  입력: BLP/SNLP 레이아웃, 0.33NA EUV 조건
  출력: 최적 소스 형상 + 초기 마스크 패턴

단계 2: 공중이미지 기반 OPC
  - 시뮬레이션 기반 CD/EPE 보정
  - 마스크 바이어스 최적화

단계 3: 레지스트 모델 보정
  - 유기 CAR 레지스트 모델
  - 금속 산화물 레지스트(MOR) 모델 비교

단계 4: 공정 창 평가
  - DOF-EL 곡선 측정
  - KLA 검사로 결함률 확인
```

### 달성된 공정 창 성능
```
BLP 레이어:
  - DOF: 119nm
  - EL: 25%
  - 도즈-to-size: 89.4 mJ/cm²
  - 피치: sub-40nm

SNLP 레이어:
  - 유사한 공정 창 조건
  - 무결함 범위(free-defect range) 확보
```

## OPC 툴 SMO 구현 관련성
- DRAM 메모리 레이어의 단일 EUV 마스크 SMO+OPC 플로우 상세 구현
- 해상도 한계(k1 < 0.4)에서의 SMO 필요성과 효과 실험적 증명
- 다양한 레지스트 타입(CAR vs MOR)을 고려한 SMO 플로우 설계
- DOF 및 EL 메트릭 기반 SMO 비용 함수 설계 참조 (DOF·EL 곱 최대화)

## 태그
`SMO`, `OPC`, `EUV`, `DRAM`, `BLP`, `SNLP`, `0.33NA`, `single_patterning`, `MOR`, `process_window`, `imec`, `SPIE`
