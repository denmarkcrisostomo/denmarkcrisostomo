<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f766e,100:0b1120&height=200&section=header&text=Denmark%20Crisostomo&fontSize=46&fontColor=e6fffb&fontAlignY=36&desc=Backend-focused%20full-stack%20developer&descSize=17&descAlignY=58&animation=fadeIn" alt="Denmark Crisostomo — backend-focused full-stack developer" width="100%">
  <br/>
  <a href="https://denmarkcrisostomo.dev">
    <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=20&duration=3000&pause=900&color=0F766E&center=true&vCenter=true&width=620&height=44&lines=NestJS+%C2%B7+PostgreSQL+%C2%B7+Stripe+Connect;Payments%2C+auth%2C+and+tenant+isolation;Multi-tenant+SaaS%2C+in+production" alt="NestJS, PostgreSQL, Stripe Connect — payments, auth, and tenant isolation">
  </a>
</div>

**Full-stack developer, backend-focused.** I work on the parts of a product that quietly ruin your week when they break — payments, auth, tenant isolation, and the data model holding all of it up.

Most of what I ship is TypeScript end to end: NestJS and PostgreSQL on the server, Next.js on the front, Stripe wherever money moves. Based in the Philippines (UTC+8), working remotely.

**Right now** I'm building a multi-tenant booking platform at Vytal Automated — per-tenant Stripe payouts, row-level security, and access codes that unlock real machines in the real world.

**I'm open to remote roles and freelance work.**

[![Portfolio](https://img.shields.io/badge/Portfolio-denmarkcrisostomo.dev-0F766E?style=for-the-badge&logo=vercel&logoColor=white)](https://denmarkcrisostomo.dev)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge)](https://www.linkedin.com/in/denmarkcrisostomo)
[![Email](https://img.shields.io/badge/Email-6D4AFF?style=for-the-badge&logo=protonmail&logoColor=white)](mailto:dev@lonewolfyyy.slmail.me)
[![Résumé](https://img.shields.io/badge/R%C3%A9sum%C3%A9-PDF-B30B00?style=for-the-badge&logo=readdotcv&logoColor=white)](./assets/DenmarkCrisostomo_Resume.pdf)

---

## Selected work

<table>
  <tr>
    <td width="50%" valign="top">
      <h3><a href="https://holyprotocol.com">Holy Protocol</a></h3>
      <a href="https://holyprotocol.com">
        <img src="./assets/holyprotocol.webp" alt="Holy Protocol" width="100%">
      </a>
      <p>A global platform for sharing and preserving faith-based testimonies. I owned the backend: REST APIs in NestJS, Better-Auth, Stripe Connect for payments and affiliate payouts, and decentralized storage on Ardrive so the records outlive whoever is hosting them.</p>
      <p>
        <img src="https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white" alt="NestJS">
        <img src="https://img.shields.io/badge/Stripe-635BFF?style=flat-square&logo=stripe&logoColor=white" alt="Stripe">
        <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL">
        <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" alt="Redis">
      </p>
      <p><b>Live in production</b> · source under NDA<br>
      <a href="https://holyprotocol.com">See it live →</a></p>
    </td>
    <td width="50%" valign="top">
      <h3><a href="https://denmarkcrisostomo.dev">UpaJuan</a></h3>
      <a href="https://denmarkcrisostomo.dev">
        <img src="./assets/upajuan.webp" alt="UpaJuan" width="100%">
      </a>
      <p>Rental management for Filipino landlords, built solo. The hard part: most rent arrives as a GCash or bank P2P transfer, and those don't come with a webhook. Solved with per-tenant QR amounts, EMV QR Ph rewriting, and a fuzzy-match fallback for reconciliation.</p>
      <p>
        <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white" alt="Next.js">
        <img src="https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white" alt="Prisma">
        <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL">
        <img src="https://img.shields.io/badge/Turborepo-EF4444?style=flat-square&logo=turborepo&logoColor=white" alt="Turborepo">
      </p>
      <p><b>Built solo</b><br>
      <a href="https://denmarkcrisostomo.dev/blog/why-i-built-upajuan">Why I built it →</a></p>
    </td>
  </tr>
</table>

<details>
<summary><b>Architecture — how Holy Protocol fits together</b></summary>
<br/>

The interesting constraints here were permanence and money. Testimonies had to outlive the company hosting them, which is what pushes content onto Ardrive rather than object storage. And affiliate payouts meant Stripe Connect, which meant the webhook handler — not the request that started the checkout — is the thing that owns the write.

```mermaid
flowchart LR
  U([Browser]) --> N[Next.js<br/>web client]
  N -->|REST| A[NestJS API]

  A --> AU[Better-Auth<br/>sessions · RBAC]
  A --> R[(Redis<br/>cache · queues)]
  A --> DB[(PostgreSQL<br/>via Prisma)]
  A --> AR[[Ardrive<br/>permanent storage]]

  A -->|Checkout · Connect| S{{Stripe}}
  S -.->|webhooks| W[/Webhook handler/]
  W --> DB
  W --> P[Affiliate payouts]
  P --> S

  classDef api fill:#0f766e,stroke:#0b5e59,color:#ffffff
  classDef store fill:#1e293b,stroke:#334155,color:#ffffff
  classDef ext fill:#635bff,stroke:#4f46e5,color:#ffffff
  class A,W api
  class DB,R,AR store
  class S ext
```

</details>

### Vytal Automated — multi-tenant SaaS

Booking and access control for self-service automated machines across multiple locations. Tenant isolation enforced with row-level security, Stripe payments wired to automated access-credential generation, and Next.js dashboards gated through a NestJS auth API. Four apps in a Turborepo.

`NestJS` · `Next.js` · `Payload CMS` · `PostgreSQL` · `Redis` · `Turborepo` · `Stripe`

Client codebase — private.

### Clairvoyance — threat intelligence

Surfaces threats and vulnerabilities before they become incidents. I built backend features on the MERN stack — JWT auth, role-based authorization, and integrations with Shodan, VirusTotal, Censys, Fofa, and Urlscan.

`MongoDB` · `Express` · `React` · `Node.js` · `TypeScript`

Earlier: **BytesMe**, a URL shortener with admin and user dashboards, and **AIROK**, a Python computer-vision bot that cut a game's resource grind by about 90% — the project that taught me automation is mostly patience.

---

## What I work with

**Backend**

![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=for-the-badge&logo=nestjs&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=for-the-badge&logo=stripe&logoColor=white)

**Frontend**

![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Vue](https://img.shields.io/badge/Vue-4FC08D?style=for-the-badge&logo=vuedotjs&logoColor=white)
![Nuxt](https://img.shields.io/badge/Nuxt-00DC82?style=for-the-badge&logo=nuxt&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![shadcn/ui](https://img.shields.io/badge/shadcn%2Fui-000000?style=for-the-badge&logo=shadcnui&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)

**Infra & tooling**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Turborepo](https://img.shields.io/badge/Turborepo-EF4444?style=for-the-badge&logo=turborepo&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-DD2C00?style=for-the-badge&logo=firebase&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![Figma](https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white)

Also comfortable in **Zod**, **Better Auth**, **Payload CMS**, **Upstash**, **Postman**, **PHP**, **Laravel**, **Python**, **Strapi**, and **WordPress**.

The short version: I'm strongest where the data model meets the money.

---

## Contribution activity

<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/denmarkcrisostomo/denmarkcrisostomo/output/github-snake-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/denmarkcrisostomo/denmarkcrisostomo/output/github-snake.svg">
    <img src="https://raw.githubusercontent.com/denmarkcrisostomo/denmarkcrisostomo/output/github-snake.svg" alt="Snake eating my contribution graph" width="100%">
  </picture>
</div>

---

## A note on the empty repo list

Most of my recent work is client code under NDA, so it isn't here. Instead of pinning toy projects, I write up the interesting problems — architecture, tradeoffs, and the parts that didn't work the first time. The write-ups on my site are the honest version of a code sample. Happy to walk through any of it on a call.

---

## Get in touch

[![Portfolio](https://img.shields.io/badge/Portfolio-denmarkcrisostomo.dev-0F766E?style=for-the-badge&logo=vercel&logoColor=white)](https://denmarkcrisostomo.dev)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge)](https://www.linkedin.com/in/denmarkcrisostomo)
[![Email](https://img.shields.io/badge/Email-6D4AFF?style=for-the-badge&logo=protonmail&logoColor=white)](mailto:dev@lonewolfyyy.slmail.me)
[![Résumé](https://img.shields.io/badge/R%C3%A9sum%C3%A9-PDF-B30B00?style=for-the-badge&logo=readdotcv&logoColor=white)](./assets/DenmarkCrisostomo_Resume.pdf)

Currently available for remote full-time roles and freelance projects.
