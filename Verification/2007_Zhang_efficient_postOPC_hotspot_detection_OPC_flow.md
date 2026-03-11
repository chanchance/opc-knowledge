# Efficient Post-OPC Lithography Hotspot Detection Using a Novel OPC Correction and Verification Flow

## 메타데이터
- **저자**: Qiaolin Zhang, Paul VanAdrichem, Kevin Lucas
- **연도**: 2007
- **게재지**: Proc. SPIE 6607, Photomask and Next-Generation Lithography Mask Technology XIV, 66072X
- **DOI/URL**: https://doi.org/10.1117/12.729016

## 핵심 요약
45nm 및 32nm 기술 노드에서 기존 OPC 모델의 불충분한 보정으로 인해 post-OPC 레이아웃에 대량의 hotspot이 발생하는 문제를 해결하기 위해, 개선된 OPC 보정과 검증 플로우를 통합하여 hotspot 검출 효율을 향상시킨 논문. 공정 모델 정확도 요구사항이 강화되는 45/32nm 노드에서 실용적인 hotspot 발견 및 처리 방법론을 제시하였다.

## 주요 기여
1. **개선된 OPC 보정-검증 통합 플로우**: OPC 보정 단계와 검증 단계를 긴밀하게 연동하여 hotspot 발견 효율 향상
2. **45/32nm 노드 공정 모델 정확도 대응**: 강화된 CD 제어 요구사항에 부합하는 더 정밀한 공정 모델 기반 OPC 검증
3. **Under-correction 기인 hotspot 해결**: 기존 OPC 모델의 under-correction으로 발생하는 hotspot을 신규 플로우로 효과적으로 포착
4. **효율적 hotspot 발견 방법론**: 전체 칩 규모에서 hotspot을 효율적으로 발견하고 처리하는 실용적 워크플로우
5. **스캐너 노출 전 사전 검증**: 마스크 제작 전 post-OPC 검증으로 hotspot 리워크 비용 절감

## 검증 방법론
- 45nm/32nm 기술 노드의 공정 모델 캘리브레이션 정확도 기반 hotspot 포착률 측정
- 기존 OPC 검증 플로우 대비 신규 통합 플로우의 hotspot 발견 수 및 false positive 비율 비교
- Under-correction hotspot 유형 분류 및 개선된 OPC 보정 후 hotspot 해소 확인
- 전체 칩 레이아웃에서의 플로우 런타임 측정

## OPC 툴 구현 관련성
- SKOPC의 OPC 보정-검증 통합 루프 설계의 기초 문헌
- `2003_Kim_hotspot_detection_postOPC_fullchip_aerial_image.md`의 초기 방법론을 45/32nm 노드로 발전시킨 후속 연구
- `2007_Lee_LRC_process_window_error_detection.md`(기수집)와 함께 2007년대 post-OPC 검증 방법론 계보 구성
- SKOPC OPC 루프에서 보정 후 즉각적 검증(in-loop verification)을 구현할 때 참조

## 태그
`Verification`, `SPIE`, `Post-OPC`, `Hotspot`, `OPC Flow`, `45nm`, `32nm`, `Process Model`, `Correction`, `Mask`
