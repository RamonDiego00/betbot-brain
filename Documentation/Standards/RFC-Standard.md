# RFC Standard

Padrao oficial para propostas e decisoes tecnicas.

## Quando abrir RFC
- Mudanca arquitetural
- Mudanca de contrato entre modulos
- Mudanca relevante de operacao/deploy
- Decisao com trade-off significativo

## Status validos
- Draft
- Review
- Accepted
- Rejected
- Superseded

## Frontmatter obrigatorio
```yaml
id: RFC-YYYY-NNN
title: ""
status: Draft
owner_role: Arquiteto
created_at: YYYY-MM-DD
updated_at: YYYY-MM-DD
related_tasks: []
supersedes: null
superseded_by: null
```

## Secoes obrigatorias
- Contexto
- Problema
- Objetivos
- Nao-objetivos
- Alternativas consideradas
- Decisao
- Impactos
- Plano de rollout
- Riscos e mitigacoes
- Metricas de sucesso

## Regras de vinculo
- RFC deve listar tasks derivadas.
- Task deve referenciar RFC mae em `related_rfc`.
