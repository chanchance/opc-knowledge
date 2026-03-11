# LLM-HD: Layout Language Model for Hotspot Detection with GDS Semantic Encoding

## 메타데이터
- **저자**: Yuyang Chen et al.
- **연도**: 2024
- **게재지**: Proceedings of the 61st ACM/IEEE Design Automation Conference (DAC 2024)
- **DOI/URL**: https://doi.org/10.1145/3649329.3658479
- **인용수**: ~10

## 핵심 요약
GDS(Graphic Database System) 파일을 픽셀 이미지로 변환하지 않고 직접 처리하여 리소그래피 핫스팟을 탐지하는 레이아웃 언어 모델(LLM-HD)을 제안한다. GDS 이진 파일의 계층적 의미 표현(hierarchical GDS semantic representation)과 사전 훈련된 NLP 모델 구조를 활용하여 이미지 변환 시 손실되는 공간적-구조적 정보를 보존한다. 정확도와 효율성 모두에서 유의미한 향상을 달성한다.

## 주요 기여
1. GDS 바이너리를 직접 처리하는 최초의 핫스팟 탐지 LLM 패러다임
2. 계층적 GDS 의미 인코딩으로 IC 설계 구조 정보 보존
3. 이미지 변환 없이 GDS 직접 처리 → 공간/구조 정보 손실 방지
4. 사전 훈련 NLP 아키텍처의 반도체 EDA 도메인 적응

## Recipe/Process Flow 상세

### 기존 핫스팟 탐지의 한계
```
기존 ML 핫스팟 탐지:
  레이아웃 GDS → 픽셀 이미지 변환 → CNN/Transformer
  픽셀 이미지 장점: 직관적, CNN 호환
  픽셀 이미지 한계:
    계층 구조 손실: 표준 셀, 셀 인스턴스 계층 무시
    공간 관계 손실: 상대 위치 정보 압축 손실
    스케일 의존: 해상도 설정에 정확도 민감
    데이터 크기: 고해상도 이미지 → 메모리 집약

GDS 직접 처리 장점:
  계층 구조 보존: Cell, Instance 계층 유지
  공간 관계 정확: 상대 위치 정밀 표현
  스케일 독립: 좌표 기반 → 해상도 무관
  압축 표현: 반복 셀 → 참조로 효율적 처리
```

### GDS 계층적 의미 인코딩
```
GDS 파일 구조:
  Library → Cells → Structures → Polygons/Paths
  계층: 최상위 설계 → 서브셀 → 기본 형상

의미 인코딩 체계:
  셀 레벨 토큰:
    cell_start, cell_end: 셀 경계
    cell_name: 셀 식별자 (표준 셀 유형)
  인스턴스 레벨 토큰:
    instance_ref: 참조 셀 이름
    instance_transform: 배치 변환 (위치, 회전, 미러)
  형상 레벨 토큰:
    polygon_points: 다각형 꼭짓점 좌표 시퀀스
    layer_info: 레이어 번호/데이터 유형

토큰 시퀀스:
  GDS 계층 → 토큰 시퀀스 변환
  예: [CELL:inv_x1] [POLYGON:Layer1:[(0,0),(100,0),...]] ...
  LLM 입력: 토큰 임베딩 시퀀스
```

### LLM 아키텍처 (NLP 적응)
```
사전 훈련 NLP 모델 구조:
  BERT 또는 GPT 계열 트랜스포머
  자기 주의(self-attention): 거리 무관 공간 관계 모델링
  위치 인코딩: 2D 좌표 인코딩 (일반 1D 시퀀스와 다름)

GDS 도메인 적응:
  사전 훈련: 대규모 GDS 데이터에서 마스크 토큰 예측
  (BERT 스타일 자기 지도 학습)
  미세 조정: 핫스팟/비핫스팟 레이블 데이터

2D 위치 인코딩:
  일반 NLP: 1D 시퀀스 위치 인코딩
  GDS-LLM: 2D 좌표 (x, y) → 위치 임베딩
  → 공간 관계 정확한 모델링

클립 레벨 분류:
  GDS 클립 → 토큰 시퀀스 → LLM → [CLS] 토큰
  [CLS] 토큰 → 분류 헤드 → 핫스팟/비핫스팟
```

### 성능 결과
```
기준: SOTA CNN/Transformer 픽셀 기반 핫스팟 탐지

정확도:
  LLM-HD: 유의미한 정확도 향상
  특히 계층 구조가 중요한 패턴 (표준 셀 경계 인접)

효율성:
  GDS 직접 처리: 이미지 변환 단계 제거 → 빠름
  반복 셀 처리: 셀 참조 활용 → 메모리 효율

일반화:
  표준 셀 계층 정보 활용 → 새 설계에 더 잘 일반화
  픽셀 모델: 셀 구조 인식 불가
```

## OPC 툴 구현 관련성
- **SKOPC GDS 핫스팟 탐지**: `skopc/core/layout_db.py` GDS 구조를 LLM 토큰 시퀀스로 변환
- **OPC 사전 선별**: LLM-HD로 OPC 전 핫스팟 클립 우선 식별 → 집중 OPC
- **GDS 의미 인코딩**: SKOPC 레이아웃 DB의 셀 계층 정보를 핫스팟 탐지에 활용
- **브리지 역할**: 핫스팟 탐지 → OPC 피드백 루프 구축

## 참고문헌
- DAC 2024 (61st ACM/IEEE Design Automation Conference)
- 관련: Bridging HSD and OPC via domain-crossing (TODAES 2025)
- 관련: ML hotspot detection (SPIE 10451, 2017)
- 관련: LLM-SRAF (DATE 2025)

## 태그
`Recipe`, `DAC`, `HotspotDetection`, `LLM`, `GDS`, `SemanticEncoding`, `Transformer`, `NLP`, `Layout`, `MachineLearning`, `2024`
