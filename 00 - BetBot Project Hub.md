# 🎰 BetBot API - Project Hub

Este é o centro de organização do ecossistema **BetBot API**, uma API REST construída com **Kotlin + Spring Boot** utilizando **Arquitetura Hexagonal**.

## 🎯 Visão Geral do Ecossistema
O BetBot API funciona como um hub de dados central que gerencia o ciclo de vida das apostas e coordena a execução via **BetBot Worker** (automação via Maestro em máquinas remotas).

---

## 📂 Navegação do Projeto

### 🏗️ [Arquitetura & Engenharia](Projetos/BetBot/Documentation/1. Architecture & Hexagonal Flow.md)
*   Arquitetura Hexagonal (Ports & Adapters)
*   Fluxo de Dados Interno (Controller -> UseCase -> Port -> Adapter)
*   Fluxo de Comunicação (API <-> Worker <-> Maestro)

### 🌐 [Referência da API & Payloads](Projetos/BetBot/Documentation/2. API Reference & Payloads.md)
*   Endpoints REST (`/api/bet`, `/api/v1/bet-decision`)
*   Modelos de Request/Response JSON
*   Swagger UI & OpenAPI

### 📦 [Domínio & Modelagem](Projetos/BetBot/Documentation/3. Domain Models & Entities.md)
*   Entidades: `Bet`, `User`, `Machine`, `Houses`, `ConfigsUser`
*   Status: `ResultBet`, `StatusMachine`

### 🧠 [BetDecision: Inteligência de Apostas](Projetos/BetBot/Documentation/4. BetDecision Intelligence.md)
*   Estratégias de IA (Over Goals, BTTS, Corners)
*   Scheduler Automático (Morning, Afternoon, Evening)
*   Integração com Telegram

### ☁️ [Infraestrutura & Deploy](Projetos/BetBot/Infrastructure/AWS & DevOps.md)
*   AWS ECS Fargate, ECR, ALB
*   Terraform & Docker
*   CI/CD GitHub Actions

---

## 📋 Gestão do Projeto
*   **Kanban de Tarefas:** [[Kanban]]
*   **Roadmap de Desenvolvimento:** [[Roadmap]]
*   **Equipe de Agentes:**
    *   [[Pedro Arquiteto]] - Design de Sistemas
    *   [[Sandro QA]] - Testes e Qualidade
    *   [[Julio Backend]] - Desenvolvimento Kotlin/Spring

---

## 🚀 Fluxo Temporal de Operação
| Horário | Job | Ação |
|---------|-----|------|
| **05:00** | `DataCollectionJob` | Coleta jogos (SofaScore) + Stats + Odds (Bet365) |
| **08:00** | `MorningDecisionJob` | IA analisa jogos 09h–13h -> WebSocket -> Maestro |
| **12:00** | `AfternoonDecisionJob` | IA analisa jogos 13h–18h -> WebSocket -> Maestro |
| **17:00** | `EveningDecisionJob` | IA analisa jogos 18h–23h -> WebSocket -> Maestro |
