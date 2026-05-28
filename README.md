<div align="center">
  
# AgentSec Twin
  
</div>
<div align="center">
  
  AI 에이전트의 권한 경로를 시뮬레이션하는 Security Ontology 기반 디지털 트윈
  
</div>
<div align="center">
  
<video src="https://github.com/user-attachments/assets/08e8cc3d-a82a-4de6-9da0-2453bc2e5eb9#t=1" width="600" controls autoplay loop muted></video>
</div>

---
## ✍️ 프로젝트 개요
| 항목 | 내용 |
| --- | --- |
| 프로젝트 정의 | AI Agent와 MCP 운영 표면의 권한 관계를 Digital Twin으로 모델링하고, 변경 영향을 시뮬레이션하는 보안 워크벤치 |
| 핵심 구조 | `Verified Twin State`, `Claimed Change / Drift`, `Simulation + Diff + Evidence`를 연결한 구조 |
| 디지털 트윈 | `Type Studio`에서 타입/관계 규칙을 정의하고, `Ontology Workbench`에서 워크스페이스 인스턴스 그래프를 편집 |
| Drift Feed | 외부 Webhook(현재 리니어만 대상), 내부 변경 신호를 기반으로 워크스페이스의 변화 흐름을 Overview에서 확인 |
| AI Assistant | AST Bot이 프로젝트 맥락 및 현재 화면 맥락을 기반으로 하네스 구성되어 Twin 구성, 스키마 작성, 시나리오 초안 생성 보조 |
| AI Simulation | `grant`, `offboarding`, `secret_exposure`, `mcp_attachment` 기본 시나리오로 Before / After 접근 경로 변화를 분석 |
| 상태 관리 | 워크스페이스 그래프 저장, 리비전 관리, 시뮬레이션 Run 저장 및 결과 재조회 지원 |
| 기술 스택 | Next.js 16, React 19, FastAPI, SQLAlchemy, SQLite 기본, Docker Compose |

---
## ✍️초기 프로젝트 기획 개요
- 프로젝트명: AgentSec Twin
- 프로젝트 기간 2026-04-01~2026-05-26
- 핵심 목적: AI 에이전트 도입 전후의 보안 영향과 경로 변화를 시뮬레이션해 의사결정을 지원
- 주요 사용자: 보안 담당자, 플랫폼 운영자, AI 도입을 검토하는 개발/운영 조직
- 핵심 차별점: 사람, AI, 도구, 데이터, 시크릿, 정책, MCP 서버를 하나의 보안 온톨로지로 모델링(팔란티어의 AIP 레퍼런스)

---
## ✍️프로젝트 소개
<img width="1280" height="720" alt="정보보호_16회차_1팀_Baseline_AgentSec Twin_결과물" src="https://github.com/user-attachments/assets/1c4740c3-c80c-4b2b-b1ea-0823960cf898" />

---
## ✍️기대 효과
<img width="1718" height="878" alt="정보보호_16회차_1팀_Baseline_AgentSec Twin_결과물 (1)" src="https://github.com/user-attachments/assets/e3ee413a-fe53-4456-832d-a84448910e1d" />

---
## 📌핵심 기능

### 1. Overview
- 워크스페이스의 Twin 상태, Drift Feed, watchlist, 최근 시뮬레이션 실행 내역을 한 화면에서 확인
- 현재 보안 구성과 최근 변경 흐름을 기준으로 후속 분석이 필요한 대상을 파악

### 2. Twin - Type Studio
- AI Agent 보안 구조를 표현하기 위한 노드 타입, 관계 타입, 필수 속성, 허용 연결 규칙 정의
- Agent, Tool, MCP, Secret, Policy, Asset 등의 구성 요소를 일관된 그래프 스키마로 관리

### 3. Twin - Ontology Workbench
- Type Studio에서 정의한 규칙을 바탕으로 실제 워크스페이스의 인스턴스 그래프 편집
- Agent, Owner, Tool, MCP, Secret, Policy, Asset 간 연결 관계를 시각적으로 구성하고 저장

### 4. AI Simulation
- 권한 부여, 오프보딩, 시크릿 노출, MCP 연결 변경 시나리오 실행
- 저장된 Workspace Graph를 기준으로 변경 전후 접근 경로와 영향 범위 분석

### 5. Runs / Result View
- 시뮬레이션 실행 결과를 Summary, Graph / Path Diff, Evidence, Report 형태로 조회
- 새롭게 열린 경로, 변경된 연결, 영향 대상, 분석 근거를 함께 확인

### 6. AST Bot
- 현재 화면 맥락을 기반으로 Twin 구성, 스키마 작성, 시나리오 초안 생성을 보조
- 사용자가 작성 중인 보안 구성과 시뮬레이션 흐름을 자연어로 탐색할 수 있도록 지원
---
## 대표 시뮬레이션 시나리오
- `grant`: AI Agent에 권한을 부여했을 때 새롭게 생기는 접근 경로를 분석
- `offboarding`: 소유자 변경 또는 퇴사 상황에서 에이전트의 ownerless 연결과 잔여 접근 경로를 확인
- `secret_exposure`: 시크릿 또는 링크 노출 시 확산 가능한 경로와 도달 가능한 자산을 분석
- `mcp_attachment`: MCP 서버 연결 시 도구 접근 범위, 자격 증명 의존성, 외부 반출 가능 경로를 시뮬레이션
---
## 프로젝트의 차별점
| 비교 관점 | 일반 보안 점검 방식 | AgentSec Twin |
| --- | --- | --- |
| 중심 질문 | 현재 설정이 안전한가 | 이 변경이 어떤 접근 경로와 영향을 만드는가 |
| 핵심 방식 | 개별 권한, 정책, 이벤트를 항목별로 확인 | Agent, Tool, MCP, Secret, Policy, Asset의 관계를 그래프로 모델링 |
| 변경 분석 | 변경 내용을 문서나 로그 단위로 확인 | 변경 전후 Workspace Graph를 비교해 경로 변화를 분석 |
| 결과 형태 | 점검 결과, 경보, 로그 중심 | Summary, Graph / Path Diff, Evidence, Report로 영향과 근거를 함께 제시 |
| AI 보안 맥락 | AI Agent를 별도 계정이나 도구 사용 주체로 취급 | AI Agent의 권한, 소유자, 연결 도구, 시크릿, MCP 서버를 하나의 Twin 구조에서 함께 확인 |

---
## 🧑‍💻팀원 소개
| 이름  | 역할  |
| --- | --- |
| 유희현 | 팀장/PM, FE/BE, AI |
| 권준현 | Infra |
| 이서현 | QA |

---
## ⚙️기술 스택
| 영역 | 기술 |
| --- | --- |
| Frontend | Next.js 16, React 19, TypeScript, Tailwind CSS, @xyflow/react, Dagre |
| Backend | FastAPI, Pydantic, SQLAlchemy, Uvicorn |
| Data / Storage | SQLite 기본 저장소, SQLAlchemy 모델, Synthetic Workspace Seed |
| Contract | Ontology Schema, Scenario Input Contract, Simulation Result Contract |
| Analysis | Workspace Graph 기반 경로 분석, Before / After Diff, 시나리오 실행 엔진 |
| AI Assistant | OpenAI-compatible API 연동 구조, AST Bot, 화면 컨텍스트 기반 질의 및 초안 작성 보조 |
| Integration | Linear Webhook 기반 change event 수집 |
| Infra / Tooling | npm workspace, Python virtualenv, Docker Compose, pytest |
---

