<p align="center">
  <img src="./banner.png" alt="Signal — When you send an SOS, Signal answers with a safe everyday life." width="100%">
</p>

<p align="center">
  <a href="https://github.com/somaus">한국어</a> | <b>English</b>
</p>

<h3 align="center">AI-powered deepfake harm prevention, detection & response</h3>

<p align="center">
  <a href="https://signal-web-rho.vercel.app"><b>Visit Signal</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/somaus/Signal-web">Web</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/somaus/Signal-server">Server</a>
</p>

<br>

## Why Signal?

Generative AI now makes it easy for anyone to create deepfake images and videos using someone else's face. Sexual crimes, defamation, and fraud that exploit deepfakes are rising fast. Yet most people don't realize their photos can be misused, and even after harm occurs, many miss the chance to respond because they don't know where to turn.

**Signal** is a one-stop service that guides you through **prevention** before you post a photo, **detection** of photos that have already spread, and **response** when harm happens.

## Key features

| Stage | Feature | Description |
| :---: | --- | --- |
| **Prevent** | Photo risk analysis | Before you post on social media, AI checks face exposure, image quality, metadata, and reverse-search risk. |
| | Image protection | Adds noise to your photo to make unauthorized use harder. |
| **Detect** | Face theft & deepfake detection | Analyzes signs of synthesis in a photo and shows the reasoning behind the result. |
| **Respond** | Anonymous chatbot | Talk with AI without revealing who you are, and get guidance on what to do next. |
| | Report support | Enter what you remember, and Signal drafts a report document ready to submit to agencies. |
| | Agency connection | Finds and connects you to counseling and reporting agencies that fit your situation. |

You can try analysis, detection, and chat without logging in. Log in to save your records.

### Service flow

```mermaid
flowchart LR
  U(("User"))

  subgraph PREVENT["① Prevent · before posting"]
    direction TB
    P1["Photo risk analysis"] --> P2["Image protection"]
  end

  subgraph DETECT["② Detect · after it spreads"]
    direction TB
    D1["Face theft & deepfake detection"] --> D2["Review the evidence"]
  end

  subgraph RESPOND["③ Respond · when harmed"]
    direction TB
    R1["Anonymous chatbot"] --> R2["Report drafting"] --> R3["Agency connection"]
  end

  U --> PREVENT
  PREVENT -- "If it has spread" --> DETECT
  DETECT -- "If harm is suspected" --> RESPOND

  classDef user fill:#2d4b66,stroke:#2d4b66,color:#ffffff
  classDef step fill:#ffffff,stroke:#9bbbd5,color:#1c3042
  class U user
  class P1,P2,D1,D2,R1,R2,R3 step
  style PREVENT fill:#edf3f8,stroke:#bcd1e3,color:#2d4b66
  style DETECT fill:#f5eaf9,stroke:#d4b7e6,color:#5f4870
  style RESPOND fill:#faf4fc,stroke:#e2bfea,color:#5f4870
```

## Multilingual support

Foreign residents in Korea can face the same harm, so both the interface and AI responses support **한국어 · English · 日本語 · 简体中文**.

## Repositories

| Repository | Description |
| --- | --- |
| [**Signal-web**](https://github.com/somaus/Signal-web) | Responsive web frontend |
| [**Signal-server**](https://github.com/somaus/Signal-server) | API server & AI integration |

## Tech stack

| Area | Technologies |
| --- | --- |
| **Frontend** | Next.js 16 (App Router) · React 19 · TypeScript · Tailwind CSS v4 · TanStack Query |
| **Backend** | Spring Boot 3.4 · Java 21 · Spring Security + JWT · MySQL |
| **AI** | Groq-hosted LLM (counseling chatbot) · Qwen-family vision model (risk analysis & deepfake detection) |
| **Infra** | Vercel (Web) · Docker (Server) |

### System architecture

```mermaid
flowchart TB
  USER(["User browser"])

  subgraph FE["Signal-web · Vercel"]
    WEB["Next.js 16 · React 19<br/>4-language UI"]
  end

  subgraph BE["Signal-server · Docker"]
    direction LR
    API["Spring Boot 3.4<br/>REST API · JWT auth"]
    RULE["Rule-based logic<br/>crisis detection · agency guidance"]
    NOISE["Image protection<br/>noise injection"]
    API --- RULE
    API --- NOISE
  end

  subgraph AI["Groq Cloud"]
    direction LR
    CHAT["Chatbot LLM<br/>counseling replies"]
    VISION["Vision model<br/>risk analysis · deepfake detection"]
  end

  DB[("MySQL")]
  FILES[("Uploaded files")]

  MAIL["Gmail SMTP<br/>verification email"]
  LAB["protection-lab<br/>adversarial noise · optional"]

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

> AI analysis and detection results come from general-purpose AI models and are provided as **reference indicators**, not definitive judgments. Crisis detection and agency guidance are handled by rule-based logic, not AI.

## Team

<table>
  <tr>
    <td align="center"><a href="https://github.com/ryusuye0n"><img src="https://github.com/ryusuye0n.png" width="88" alt="ryusuye0n"><br><sub><b>Suyeon Ryu</b></sub></a></td>
    <td align="center"><a href="https://github.com/hyooeunn"><img src="https://github.com/hyooeunn.png" width="88" alt="hyooeunn"><br><sub><b>Hyoeun Lee</b></sub></a></td>
    <td align="center"><a href="https://github.com/jyx-07"><img src="https://github.com/jyx-07.png" width="88" alt="jyx-07"><br><sub><b>jyx-07</b></sub></a></td>
    <td align="center"><a href="https://github.com/hyeinggu"><img src="https://github.com/hyeinggu.png" width="88" alt="hyeinggu"><br><sub><b>hyeinggu</b></sub></a></td>
  </tr>
</table>

<br>

<p align="center"><sub>Soma + Us. Building things together.</sub></p>
