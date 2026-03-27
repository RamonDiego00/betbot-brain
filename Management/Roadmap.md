# 🗺️ BetBot Roadmap

## Fase 1: Fundação & Core API (✅ Concluído)
- [x] Definição da Arquitetura Hexagonal.
- [x] Configuração do Spring Boot & Kotlin.
- [x] Implementação dos modelos de domínio (`Bet`, `User`, `Machine`).
- [x] Endpoints básicos de CRUD de apostas.

## Fase 2: BetDecision Intelligence (🚧 Em Andamento)
- [ ] Implementar `DataCollectionJob` para coleta automática (SofaScore/Bet365).
- [ ] Desenvolver estratégias de IA: Over Goals, BTTS e Corners.
- [ ] Configurar o Scheduler automático (Morning, Afternoon, Evening).
- [ ] Integração com o bot do Telegram para alertas.

## Fase 3: Worker & Automação Maestro
- [ ] Finalizar integração via WebSocket com o BetBot Worker.
- [ ] Testar execução de automação em máquinas remotas via Maestro.
- [ ] Implementar feedback de resultados (GANHOU/PERDEU) via Worker -> API.

## Fase 4: Infraestrutura & Cloud
- [ ] Provisionar recursos AWS via Terraform (ECS, ECR, ALB, CloudWatch).
- [ ] Configurar Pipeline de CI/CD no GitHub Actions.
- [ ] Deploy em produção (AWS ECS Fargate).
