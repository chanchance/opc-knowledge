# OPC and Verification Accuracy Enhancement Using the 2D Wafer Image for the Low-k1 Memory Devices

## 메타데이터
- **저자**: Yong-Chan Ban, Dong-Yoon Lee, Ji-Suk Hong, Moon-Hyun Yoo, Jeong-Taek Kong
- **연도**: 2006
- **게재지**: Proc. SPIE 6154, Optical Microlithography XIX, 61540J
- **DOI/URL**: https://doi.org/10.1117/12.656280

## 핵심 요약
기존 1D CD 측정 중심의 OPC 모델 생성에서 벗어나, 2D SEM 이미지 또는 리고러스 시뮬레이션 이미지를 모델 피팅에 직접 활용하는 2D 이미지 기반 OPC 모델 캘리브레이션 및 검증 방법론을 제안한 논문. "2D 웨이퍼 이미지 하나가 수천 건의 CD 측정을 대체한다"는 핵심 명제로, 라인엔드, 컨택, 코너 등 2D 구조에서의 모델 오차를 획기적으로 줄였다.

## 주요 기여
1. **2D 이미지 기반 모델 피팅**: SEM 이미지 또는 리고러스 시뮬레이션 이미지를 OPC 모델 캘리브레이션 데이터로 직접 활용
2. **2D 구조 모델 오차 감소**: 라인엔드, 컨택, 코너 등 1D CD 측정으로 포착하기 어려운 2D 형상에서의 모델 오차 감소
3. **측정 부담 감소**: 수백 건의 1D CD 측정 대신 소수의 2D SEM 이미지로 동등하거나 우수한 모델 정확도 달성
4. **저-k1 메모리 소자 적용**: 삼성 메모리 디바이스의 저-k1 리소그래피 공정에서 실증
5. **OPC 검증 정확도 향상**: 2D 이미지 기반 모델을 OPC 검증에 적용하여 컨투어 예측 정확도 개선

## 검증 방법론
- 삼성 저-k1 메모리 공정의 실제 SEM 이미지를 2D 모델 캘리브레이션에 활용
- 1D CD 기반 모델 vs. 2D 이미지 기반 모델의 EPE 분포 비교
- 라인엔드, 컨택, 코너 등 2D 취약 구조에서의 모델 예측 정확도 개선량 정량화
- OPC 검증 컨투어와 실제 SEM 컨투어 오버레이 비교

## OPC 툴 구현 관련성
- SKOPC의 OPC 모델 캘리브레이션 모듈에서 2D SEM 이미지를 캘리브레이션 데이터로 지원하는 기능 설계의 초석
- `2022_IEEE_OPC_model_accuracy_aerial_image_stability.md`의 에어리얼 이미지 방법론의 선행 아이디어 제공
- `2023_Latinwo_OPC_modeling_accuracy_resist_deformation.md`와 함께 OPC 모델 정확도 향상 방법론 계보 구성
- SKOPC Calibration 모듈에서 "CD only" vs. "contour/image" 캘리브레이션 모드 설계 시 근거 문헌

## 태그
`Verification`, `SPIE`, `OPC Model`, `Calibration`, `2D Image`, `SEM`, `Low-k1`, `Memory`, `EPE`, `Contour`
