# ACK 멀티클러스터 GitOps PoC

ACK 기반 멀티클러스터 GitOps 테스트 및 운영 모델 검증을 위한 저장소입니다.

---

# 프로젝트 목표

본 프로젝트는 Alibaba Cloud ACK 환경에서 GitOps 기반 멀티클러스터 운영 구조를 검증하는 것을 목표로 합니다.

다음 항목들을 단계적으로 테스트합니다.

- Argo CD 기반 멀티클러스터 관리
- Git Repository 기반 선언형 운영
- NetworkPolicy 중앙 관리
- ARMS Prometheus 기반 모니터링
- SLS 기반 로그 저장 및 분석
- Hubble 기반 네트워크 흐름 시각화
- Helm / Kustomize 기반 애플리케이션 관리
- App of Apps 패턴 검증
- RBAC / SSO / DR 구조 검토

---

# 전체 구성도

```text
Git Repository
      ↓
   Argo CD
  ↙       ↘
ACK-A   ACK-B
  ↓       ↓
Policy  Policy
  ↓
Monitoring / Logging
```

---

# 클러스터 구성

| Cluster | 역할 |
|---|---|
| cluster-a | Argo CD Control Plane |
| cluster-b | Managed Cluster |

---

# Repository 구조

```text
.
├── apps
├── base
├── bootstrap
└── clusters
```

## clusters/

클러스터별 배포 상태를 관리합니다.

예시:

```text
clusters/
 ├── cluster-a
 └── cluster-b
```

---

## base/

여러 클러스터에서 공통으로 사용하는 리소스를 관리합니다.

예시:

- Namespace
- NetworkPolicy
- Monitoring
- Logging

---

## apps/

실제 애플리케이션 정의를 관리합니다.

예시:

- Deployment
- Service
- Ingress
- Helm Values

---

## bootstrap/

Argo CD 및 GitOps 초기 구성 리소스를 관리합니다.

---

# GitOps 운영 원칙

본 저장소는 GitOps 운영 원칙을 따릅니다.

## 핵심 원칙

- Git Repository를 Source of Truth로 사용
- kubectl 직접 apply 최소화
- Git 변경을 통해 운영 상태 관리
- 선언형(Declarative) YAML 기반 구성
- 클러스터 상태와 Git 상태 일치 유지

---

# 사용 예정 기술 스택

| 영역 | 기술 |
|---|---|
| Kubernetes | ACK |
| GitOps | Argo CD |
| Monitoring | ARMS Prometheus |
| Logging | SLS |
| Network | Terway |
| Observability | Hubble |
| Packaging | Helm |
| Overlay | Kustomize |

---

# 향후 테스트 예정 항목

- Multi Cluster GitOps
- NetworkPolicy 운영 모델
- Drift Detection
- Auto Sync / Self Heal
- App of Apps 패턴
- Helm 기반 배포
- Kustomize Overlay
- Hubble Flow 분석
- SLS 로그 분석
- GitOps 기반 운영 자동화

---

# 목적

본 저장소는 단순 Kubernetes 실습이 아닌,

ACK 기반 클라우드 네이티브 멀티클러스터 GitOps 운영 모델을 이해하고 검증하기 위한 PoC 환경 구축을 목표로 합니다.