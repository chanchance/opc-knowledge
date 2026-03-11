# EUV Mask Synthesis with Rigorous ILT for Process Window Improvement

## 메타데이터
- **저자**: Kyle Braam, Kosta Selinidis, Wolfgang Hoppe, Hongyuan Cai, Guangming Xiao
- **소속**: Synopsys, Inc. (미국) / Synopsys GmbH (독일)
- **연도**: 2019
- **게재지**: Proc. SPIE 10962, Design-Process-Technology Co-optimization for Manufacturability XIII, 109620P (5 April 2019)
- **DOI/URL**: https://doi.org/10.1117/12.2515156

## 핵심 요약
엄격한(rigorous) EUV 리소그래피 모델과 ILT를 결합한 EUV 마스크 합성 방법을 제안한다. EUV 공정 창 및 CD 제어 향상을 위한 엄격한 DUV/EUV ILT 기능의 구체적 장점을 여러 응용 사례에서 시연한다. 레지스트 프로파일 최적화, 레지스트 디스컴밍(descumming) 공정 창 개선 등에서 정량적 이점을 보고한다.

## 주요 기여
1. **엄격한 EUV ILT 프레임워크**: 근사 모델이 아닌 엄격한 EUV 물리 모델 기반 ILT 구현
2. **레지스트 프로파일 최적화**: 레지스트 top-loss 및 descumming을 위한 ILT 적용
3. **공정 창 향상**: 엄격한 ILT로 기존 OPC 대비 EUV 공정 창 정량적 개선
4. **DUV/EUV 통합 ILT**: 동일 프레임워크에서 DUV와 EUV 모두 지원하는 범용 ILT

## 알고리즘/수식
### 엄격한 EUV ILT 비용 함수
```
min_{M} Σ_i ||I_sim(M, S, z_i, d_i) - I_target||²_w + λ·MRC(M)

여기서:
- M: EUV 마스크 패턴 (반사형)
- S: 조명 소스
- z_i: i번째 포커스 조건
- d_i: i번째 도즈 조건
- I_sim: 엄격한 EMF + 레지스트 모델 기반 시뮬레이션
- MRC(M): 마스크 제조 규칙 제약 (Mask Rule Check)
- ||·||²_w: 가중 L2 노름
```

### 엄격한 EUV 모델 구성요소
1. **EMF(전자기장) 계산**: RCWA 또는 FDTD 기반 EUV 마스크 회절 계산
2. **Hopkins 이미징**: 부분 간섭(partial coherence) 이미징 공식
3. **레지스트 모델**: 화학 증폭 레지스트(CAR) 3D 프로파일 시뮬레이션
   - 레지스트 top-loss: 수직 방향 레지스트 손실 최적화
   - descumming: 하부 잔류 레지스트 제거 최적화

### 최적화 방법
- 경사 기반 ILT: 비용 함수의 마스크에 대한 해석적 기울기 계산
- 교번 최소화: 마스크 최적화 ↔ 공정 창 평가 반복

## OPC 툴 SMO 구현 관련성
- SMO와 ILT 결합: 소스 최적화 후 엄격한 ILT 마스크 합성 파이프라인
- EUV 레지스트 3D 프로파일 최적화: 단순 CD 최적화를 넘어 레지스트 형상 최적화
- 공정 창 인식 ILT: 다중 포커스-도즈 조건에서 동시 최적화
- SKOPC 마스크 합성 모듈에서 엄격한 EUV 물리 모델 통합 필요성 시사

## 태그
`ILT`, `EUV`, `OPC`, `rigorous_model`, `resist_model`, `process_window`, `EMF`, `RCWA`, `DTCO`, `SPIE`
