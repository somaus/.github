<p align="center">
  <img src="./banner.png" alt="Signal — 당신이 보낸 구조 신호, Signal이 안전한 일상으로 답합니다." width="100%">
</p>

<p align="center">
  <b>한국어</b> | <a href="https://github.com/somaus/.github/blob/main/profile/README.en.md">English</a>
</p>

<h3 align="center">AI 기반 딥페이크 피해 예방·탐지·대응 서비스</h3>

<p align="center">
  <a href="https://signal-web-rho.vercel.app"><b>서비스 바로가기</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/somaus/Signal-web">Web</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/somaus/Signal-server">Server</a>
</p>

<br>

## 왜 Signal인가요?

생성형 AI가 발전하면서 누구나 손쉽게 타인의 얼굴을 합성한 딥페이크 이미지·영상을 만들 수 있게 되었습니다. 딥페이크를 악용한 성범죄·명예훼손·사기 피해는 빠르게 늘고 있지만, 대부분의 사람은 자신의 사진이 악용될 수 있다는 사실을 모르고, 피해를 입은 뒤에도 어디에 알려야 할지 몰라 대응 시점을 놓칩니다.

**Signal**은 사진을 올리기 전의 **예방**, 이미 퍼진 사진의 **탐지**, 피해가 생겼을 때의 **대응**까지 하나의 흐름으로 돕는 원스톱 서비스입니다.

## 주요 기능

| 단계 | 기능 | 설명 |
| :---: | --- | --- |
| **예방** | 사진 위험도 분석 | SNS에 올리기 전, AI가 얼굴 노출도·이미지 품질·메타데이터·역검색 위험을 진단합니다. |
| | 이미지 보호 처리 | 사진에 노이즈를 넣어 무단 활용을 어렵게 합니다. |
| **탐지** | 얼굴 도용·딥페이크 탐지 | 사진의 합성 흔적을 분석하고 판단 근거를 함께 보여줍니다. |
| **대응** | 익명 상담 챗봇 | 신원을 밝히지 않고 AI와 상담하며 다음 행동을 안내받습니다. |
| | 신고 지원 | 기억나는 내용만 입력하면 기관에 제출하기 좋은 신고 문서 초안을 만들어 줍니다. |
| | 기관 연결 | 피해 상황에 맞는 상담·신고 기관을 찾아 바로 연결합니다. |

로그인 없이도 분석·탐지·상담을 체험할 수 있고, 기록을 저장하려면 로그인합니다.

### 서비스 흐름

```mermaid
flowchart LR
  U(("사용자"))

  subgraph PREVENT["① 예방 · 사진 올리기 전"]
    direction TB
    P1["사진 위험도 분석"] --> P2["이미지 보호 처리"]
  end

  subgraph DETECT["② 탐지 · 이미 퍼졌을 때"]
    direction TB
    D1["얼굴 도용·딥페이크 탐지"] --> D2["판단 근거 확인"]
  end

  subgraph RESPOND["③ 대응 · 피해가 생겼을 때"]
    direction TB
    R1["익명 상담 챗봇"] --> R2["신고 문서 작성"] --> R3["기관 연결"]
  end

  U --> PREVENT
  PREVENT -- "이미 퍼졌다면" --> DETECT
  DETECT -- "피해가 의심되면" --> RESPOND

  classDef user fill:#2d4b66,stroke:#2d4b66,color:#ffffff
  classDef step fill:#ffffff,stroke:#9bbbd5,color:#1c3042
  class U user
  class P1,P2,D1,D2,R1,R2,R3 step
  style PREVENT fill:#edf3f8,stroke:#bcd1e3,color:#2d4b66
  style DETECT fill:#f5eaf9,stroke:#d4b7e6,color:#5f4870
  style RESPOND fill:#faf4fc,stroke:#e2bfea,color:#5f4870
```

## 다국어 지원

국내에 거주하는 외국인도 같은 피해를 겪을 수 있기에, 화면과 AI 응답 모두 **한국어 · English · 日本語 · 简体中文**을 지원합니다.

## 저장소

| 저장소 | 설명 |
| --- | --- |
| [**Signal-web**](https://github.com/somaus/Signal-web) | 반응형 웹 프론트엔드 |
| [**Signal-server**](https://github.com/somaus/Signal-server) | API 서버 · AI 연동 |

## 기술 스택

| 구분 | 사용 기술 |
| --- | --- |
| **Frontend** | Next.js 16 (App Router) · React 19 · TypeScript · Tailwind CSS v4 · TanStack Query |
| **Backend** | Spring Boot 3.4 · Java 21 · Spring Security + JWT · MySQL |
| **AI** | Groq 호스팅 LLM (상담 챗봇) · Qwen 계열 비전 모델 (위험도 분석·딥페이크 탐지) |
| **Infra** | Vercel (Web) · Docker (Server) |

### 시스템 구조

```mermaid
flowchart TB
  USER(["사용자 브라우저"])

  subgraph FE["Signal-web · Vercel"]
    WEB["Next.js 16 · React 19<br/>4개 언어 화면"]
  end

  subgraph BE["Signal-server · Docker"]
    direction LR
    API["Spring Boot 3.4<br/>REST API · JWT 인증"]
    RULE["규칙 기반 로직<br/>위기 감지 · 기관 안내"]
    NOISE["이미지 보호<br/>노이즈 삽입"]
    API --- RULE
    API --- NOISE
  end

  subgraph AI["Groq Cloud"]
    direction LR
    CHAT["챗봇 LLM<br/>상담 답변"]
    VISION["비전 모델<br/>위험도 분석 · 딥페이크 탐지"]
  end

  DB[("MySQL")]
  FILES[("업로드 파일")]

  MAIL["Gmail SMTP<br/>인증번호 메일"]
  LAB["protection-lab<br/>적대적 노이즈 · 선택"]

  USER --> WEB
  WEB -- "REST · Accept-Language" --> API
  API --> AI
  API --> DB
  API --> FILES
  API --> MAIL
  API -.-> LAB

  classDef core fill:#2d4b66,stroke:#2d4b66,color:#ffffff
  classDef inner fill:#ffffff,stroke:#9bbbd5,color:#1c3042
  classDef ext fill:#ffffff,stroke:#bc9dcf,color:#5f4870
  classDef opt fill:#ffffff,stroke:#bc9dcf,color:#86689c,stroke-dasharray:4 3
  class WEB,API core
  class RULE,NOISE,USER inner
  class CHAT,VISION,DB,FILES,MAIL ext
  class LAB opt
  style FE fill:#edf3f8,stroke:#bcd1e3,color:#2d4b66
  style BE fill:#edf3f8,stroke:#bcd1e3,color:#2d4b66
  style AI fill:#faf4fc,stroke:#e2bfea,color:#5f4870
```

> AI 분석·탐지 결과는 범용 AI 모델의 판단으로, 확정 판정이 아닌 **참고 지표**로 제공합니다. 위기 감지와 기관 안내는 AI가 아닌 규칙 기반 로직이 담당합니다.

## Team

<table>
  <tr>
    <td align="center"><a href="https://github.com/ryusuye0n"><img src="https://github.com/ryusuye0n.png" width="88" alt="ryusuye0n"><br><sub><b>류수연</b></sub></a></td>
    <td align="center"><a href="https://github.com/hyooeunn"><img src="https://github.com/hyooeunn.png" width="88" alt="hyooeunn"><br><sub><b>이효은</b></sub></a></td>
    <td align="center"><a href="https://github.com/jyx-07"><img src="https://github.com/jyx-07.png" width="88" alt="jyx-07"><br><sub><b>종윤</b></sub></a></td>
    <td align="center"><a href="https://github.com/hyeinggu"><img src="https://github.com/hyeinggu.png" width="88" alt="hyeinggu"><br><sub><b>hyeinggu</b></sub></a></td>
  </tr>
</table>

<br>

<p align="center"><sub>Soma + Us. Building things together.</sub></p>
