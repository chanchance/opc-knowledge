# Rounded-Corner Aware OPC for Convergency and Lithography Performance Improving

## 메타데이터
- **저자**: Ruihua Liu, Fu Li, Chunlong Yu, Jingjing Fan, Yu Mu, Song Sun, Chong Wang, Jiangliu Shi, Qingchen Cao
- **연도**: 2023
- **게재지**: Proc. SPIE 12751, Photomask Technology 2023, 1275115
- **DOI/URL**: https://doi.org/10.1117/12.2686228

## 핵심 요약
마스크 코너 라운딩(mask corner rounding)을 OPC 모델에 직접 통합한 RC-OPC(Rounded Corner Aware OPC) 기법을 제안한다. 기존 OPC는 마스크 모서리가 이상적인 직각으로 처리되나, 실제 마스크 제조 공정에서 코너는 라운딩된다. RC-OPC는 이 코너 라운딩 효과를 OPC 시뮬레이션과 보정에 반영하여 수렴성(convergency), 리소그래피 성능, 패턴 충실도를 동시에 향상시킨다.

## 주요 기여
1. **RC-OPC 방법론**: 마스크 코너 라운딩을 OPC 플로우에 통합하는 최초의 체계적 접근법
2. **수렴성 향상**: 코너 라운딩 인식으로 OPC 반복 계산의 수렴 안정성 개선
3. **리소그래피 성능 향상**: 코너 라운딩 효과 보정으로 실제 웨이퍼 CD 정확도 향상
4. **패턴 충실도 개선**: 다양한 크기의 사각형 패턴에서 코너 라운딩 보상 OPC 적용
5. **메모리 공정 적용**: Beijing Superstring Academy of Memory Technology에서 메모리 레이어 OPC에 적용

## Recipe/Flow 상세
- **RC-OPC 플로우**:
  1. **코너 라운딩 모델 캘리브레이션**:
     - 다양한 크기의 직각 패턴에서 실제 마스크 코너 라운딩 측정
     - 패턴 크기, 마스크 공정 조건에 따른 코너 라운딩 반경(r) 모델 구성
     - SEM 또는 CD-SEM으로 코너 라운딩 파라미터 추출
  2. **RC-OPC 시뮬레이션 모델 구성**:
     - 기존 직각 마스크 모델에 코너 라운딩 효과 추가
     - 코너 라운딩된 마스크 형상의 광학 이미지 시뮬레이션
     - 현상 후 패턴 CD 예측에 코너 라운딩 영향 반영
  3. **OPC 보정 전략 수정**:
     - 코너 영역에서 세리프(serif) 또는 해머헤드 추가 방식 조정
     - 코너 라운딩으로 인한 CD 손실 사전 보상
     - 직선 에지와 코너 영역의 OPC 파라미터 분리 최적화
  4. **수렴성 개선**:
     - 코너 라운딩 인식으로 시뮬레이션-측정 불일치 감소
     - EPE 잔차 감소 → 더 빠른 수렴
     - 반복 횟수 감소로 런타임 단축 효과
  5. **검증**:
     - 다양한 패턴 크기에서 RC-OPC vs. 기존 OPC 비교
     - 웨이퍼 프린팅 결과로 패턴 충실도 검증
- **코너 라운딩 특성**:
  - 마스크 패턴 크기가 작을수록 코너 라운딩 영향 증가
  - E-beam 마스크 기록 후 현상 공정에서 발생
  - MPC(Mask Process Correction)와의 상호작용 고려 필요
- **적용 대상**: 메모리(DRAM/NAND) 레이어, 특히 규칙적 어레이 패턴

## OPC 툴 구현 관련성
- SKOPC OPC 시뮬레이션 엔진에서 코너 라운딩 마스크 모델 추가
- `corner_rounding_model.py`: 마스크 코너 라운딩 파라미터 모델 및 OPC 시뮬레이션 통합
- 메모리 레이어 OPC 레시피에서 RC-OPC 옵션 활성화
- 코너 영역 OPC 파라미터 분리 처리 로직 구현

## 태그
`OPC`, `CornerRounding`, `MaskModel`, `PatternFidelity`, `Memory`, `DRAM`, `Convergence`, `Photomask`, `SPIE`, `2023`
