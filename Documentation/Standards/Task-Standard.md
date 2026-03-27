# Task Standard

Padrao oficial para tarefas executadas por agentes.

## Frontmatter obrigatorio
```yaml
id: TASK-YYYY-NNN
title: ""
status: TODO
priority: P0|P1|P2|P3
owner_role: Arquiteto|Backend|QA|DevOps|Produto
requested_by: ""
created_at: YYYY-MM-DD
updated_at: YYYY-MM-DD
related_rfc: null|RFC-YYYY-NNN
depends_on: []
acceptance_criteria: []
context_links: []
```

## Corpo obrigatorio
1. Contexto
2. Objetivo
3. Escopo (in/out)
4. Plano de execucao
5. Checklist de aceite
6. Log de execucao do agente
7. Resultado e hand-off

## Regra operacional
- Proibido executar sem `task_id`.
- Toda atualizacao relevante deve ser registrada no log da task.
- Ao concluir, mover arquivo para pasta de status correspondente.

## Template sugerido
```markdown
---
id: TASK-YYYY-NNN
title: ""
status: TODO
priority: P1
owner_role: Backend
requested_by: ""
created_at: YYYY-MM-DD
updated_at: YYYY-MM-DD
related_rfc: null
depends_on: []
acceptance_criteria:
  - ""
context_links:
  - ""
---

# TASK-YYYY-NNN: Titulo

## Contexto

## Objetivo

## Escopo in
- 

## Escopo out
- 

## Plano de execucao
- [ ]

## Checklist de aceite
- [ ]

## Log de execucao do agente
- YYYY-MM-DD HH:mm - Inicio da execucao.

## Resultado e hand-off
- Status:
- Proximo responsavel:
```
