# Cloud Flight Plan for Post-Tapeout Flow Jobs

## 메타데이터
- **저자**: Pascal Gilgenkrantz, Bassem Riad, Maram Salah, Azim Siddique
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540O (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010142

## 핵심 요약
반도체 포스트-테이프아웃 플로우(PTOF) 작업을 클라우드(AWS)로 이전하는 방법론을 제시한다. Siemens EDA Reference Environment를 AWS에 구축하여 OPC-MPC-MDP 포스트-테이프아웃 플로우를 실행하며, 동적 작업 스케일링과 AWS Spot Instance를 활용한 비용 효율적이고 대규모 확장 가능한 Calibre FullScale 실행을 구현한다.

## 주요 기여
1. **클라우드 OPC 플로우**: AWS 기반 Calibre OPC-MPC-MDP 포스트-테이프아웃 플로우 구현
2. **동적 스케일링**: 작업 부하에 따른 동적 클라우드 자원 할당
3. **비용 최적화**: AWS Spot Instance 활용으로 OPC 컴퓨팅 비용 절감
4. **Calibre FullScale**: 대규모 전체 칩 OPC를 클라우드에서 실행하는 확장성 입증

## 알고리즘/수식
### 클라우드 OPC 플로우 아키텍처
```
포스트-테이프아웃 플로우 (PTOF):
  OPC → MPC → MDP
  OPC: Optical Proximity Correction (광학 근접 보정)
  MPC: Mask Process Correction (마스크 공정 보정)
  MDP: Mask Data Preparation (마스크 데이터 준비)

클라우드 실행 환경:
  Siemens EDA Reference Environment on AWS
  - EC2 인스턴스: 고성능 컴퓨팅 (C/M/R 계열)
  - Spot Instance: 비용 절감 (최대 90%)
  - Auto Scaling: 작업 부하 기반 자동 스케일링

Calibre FullScale:
  전체 칩 OPC 분할 실행
  병렬 처리: N_core × N_node 스케일 아웃
  → 런타임 선형 감소: T ∝ 1/(N_core × N_node)
```

### 성능 및 비용 분석
```
확장성:
  로컬 클러스터 대비 클라우드: 무제한 확장 가능
  TAT (Turn-Around Time) 단축: 온디맨드 자원 확보

비용 모델:
  Cost = ∑ (instance_hours × price_per_hour)
  Spot Instance 활용 시 비용 60-80% 절감
  온디맨드 대비 TAT 유지하며 비용 최적화

OPC 품질 검증:
  클라우드 실행 결과 = 로컬 실행 결과
  동일한 Calibre 엔진 → 재현성 보장
```

## OPC 툴 SMO 구현 관련성
- 클라우드 OPC 실행: SKOPC의 클라우드 배포 전략에 참고
- OPC-MPC-MDP 플로우: 마스크 제조를 포함한 전체 포스트-테이프아웃 플로우 통합
- 대규모 확장성: 전체 칩 SMO/OPC의 클라우드 기반 병렬 실행 참고
- 비용 최적화: 클라우드 Spot Instance 활용한 OPC 컴퓨팅 비용 최소화

## 태그
`OPC`, `cloud`, `AWS`, `Calibre`, `Siemens`, `post_tapeout`, `MPC`, `MDP`, `FullScale`, `scalability`, `SPIE`, `2024`
