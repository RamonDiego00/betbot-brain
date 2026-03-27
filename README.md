# 🎰 BetBot API

API REST construída com **Kotlin + Spring Boot** utilizando **Arquitetura Hexagonal (Ports & Adapters)**. Responsável por gerenciar apostas e estabelecer comunicação com o **BetBot Worker** — um serviço privado que se conecta via WebSocket a máquinas remotas e executa automações de apostas utilizando o **Maestro**.

---

## 📋 Índice

- [Visão Geral](#-visão-geral)
- [Arquitetura](#-arquitetura)
- [Tecnologias](#-tecnologias)
- [Modelos de Domínio](#-modelos-de-domínio)
- [Endpoints da API](#-endpoints-da-api)
- [Payloads JSON](#-payloads-json)
- [Como Executar](#-como-executar)
- [Docker](#-docker)
- [Deploy na AWS](#-deploy-na-aws)
- [Integração com BetBot Worker](#-integração-com-betbot-worker)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [BetDecision API](#-betdecision-api)
- [Fluxo Temporal](#-fluxo-temporal-completo)

---

## 🎯 Visão Geral

O **BetBot API** é o componente central do ecossistema de automação de apostas. Ele funciona como um hub de dados que:

1. **Recebe e armazena** informações sobre apostas (jogadores, casas de apostas, odds, valores).
2. **Fornece dados via REST** para que o **BetBot Worker** saiba em quais jogadores realizar apostas.
3. **Gerencia o ciclo de vida das apostas**, rastreando resultados (`GANHOU`, `PERDEU`, `PENDENTE`).

### Fluxo de Comunicação

```
┌─────────────┐       REST/JSON        ┌───────────────┐     WebSocket      ┌──────────────┐
│  BetBot API │ ◄────────────────────► │ BetBot Worker │ ◄────────────────► │   Máquina    │
│ (este repo) │   Dados das apostas    │   (privado)   │   Automação via   │   Remota     │
│             │   e jogadores          │               │     Maestro       │              │
└─────────────┘                        └───────────────┘                    └──────────────┘
```

---

## 🏗 Arquitetura

O projeto segue a **Arquitetura Hexagonal (Ports & Adapters)**, garantindo desacoplamento entre a lógica de negócio e a infraestrutura.

### Fluxo de Dados Interno
`Controller → BetUseCase (port in) → BetService → BetPort (port out) → PersistenceBetAdapter → JPA Repository → H2 Database`

---

## 🛠 Tecnologias

| Tecnologia | Versão | Descrição |
|---|---|---|
| **Kotlin** | 1.9.25 | Linguagem principal |
| **Spring Boot** | 3.5.0 | Framework web e DI |
| **Spring Data JPA** | — | ORM e persistência |
| **H2 Database** | — | Banco de dados em memória |
| **Jackson Kotlin** | — | Serialização/deserialização JSON |
| **Java (JVM)** | 21 | Runtime |
| **Gradle (Kotlin DSL)** | — | Build tool |
| **Docker** | — | Containerização |
| **Terraform** | — | Infraestrutura como Código (IaC) |
| **AWS ECS Fargate** | — | Orquestração de containers |
| **AWS ECR** | — | Registro de imagens Docker |
| **AWS ALB** | — | Load Balancer |

---

## 📦 Modelos de Domínio

### Bet (Aposta)
- `id`: `Long`
- `userId`: `Long`
- `houseId`: `Long`
- `amount`: `Double`
- `odd`: `Double`
- `result`: `GANHOU`, `PERDEU`, `PENDENTE`
- `date`: `LocalDateTime`

### User (Usuário)
- `id`, `name`, `email`
- `houses`: `List<Houses>`
- `machines`: `List<Machine>`
- `configs`: `ConfigsUser`

---

## 🌐 Endpoints da API

Base URL: `http://localhost:8080`

| Método | Endpoint | Descrição |
|---|---|---|
| `POST` | `/api/bet` | Criar uma nova aposta |
| `GET` | `/api/bet/{id}` | Buscar aposta por ID |
| `GET` | `/api/bet` | Listar todas as apostas |
| `GET` | `/actuator/health` | Health Check |

---

## 🤖 BetDecision API — Geração Inteligente de Apostas

O `betbotAPI` é responsável por todo o pipeline de inteligência: coleta de dados, análise estatística, decisão de apostas e envio ao `betbot-worker` via WebSocket.

### Estratégias de Decisão da IA

| Estratégia | Condições | Mercado | Seleção |
|-----------|-----------|---------|---------|
| Over Goals | Expectativa ≥ 2.8 E média chutes ≥ 3.0 | Total Goals | Over 1.5 |
| BTTS | Taxa BTTS > 60% E (chutes ≥ 3.0 OU média gols ≥ 1.2) | BTTS | Yes |
| Corners | Total escanteios > 10 E média time ≥ 4.5 | Corners | Over 9.5 |

### Scheduler Automático

| Período | Horário do Job | Janela de Jogos |
|---------|---------------|-----------------|
| MORNING | 08:00 | 09:00 – 13:00 |
| AFTERNOON | 12:00 | 13:00 – 18:00 |
| EVENING | 17:00 | 18:00 – 23:00 |

---

## 🕐 Fluxo Temporal Completo

- **05:00**: `DataCollectionJob` - Coleta jogos (SofaScore) + stats + odds.
- **08:00**: `MorningDecisionJob` - IA analisa jogos 09h–13h.
- **12:00**: `AfternoonDecisionJob` - IA analisa jogos 13h–18h.
- **17:00**: `EveningDecisionJob` - IA analisa jogos 18h–23h.

---

## 📨 Integração com Telegram

Endpoint: `POST /api/v1/bet-decision/generate-today-and-send`
- Envia JSONs gerados para o bot configurado.
- Se > 4096 chars, envia como arquivo `.json`.

---

## ⚙️ CI/CD & Secrets

- **GitHub Actions**: `.github/workflows/ci.yml`
- **Gates**: Build, Unit Tests (70% coverage), Lint (ktlint), Integration Tests.
- **Banco**: H2 para unitários, Postgres container para integração.

---

## 📋 Gestão
- Kanban: [[Kanban]]
- Roadmap: [[Roadmap]]
- Time: [[Pedro Arquiteto]], [[Sandro QA]], [[Julio Backend]]
