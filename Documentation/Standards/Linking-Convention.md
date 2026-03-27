# Linking Convention

Convencoes de linkagem para Obsidian e rastreabilidade entre artefatos.

## Formato de links
- Preferir wiki links: `[[caminho/arquivo|alias]]`
- IDs sempre explicitos no texto: `TASK-*`, `RFC-*`

## Regras de rastreabilidade
- Task sempre aponta para role dona (`owner_role`).
- Task aponta para RFC quando houver decisao tecnica.
- RFC lista tasks derivadas.
- Handoffs devem citar proxima role responsavel.

## Tags sugeridas
- `#task`
- `#rfc`
- `#agent`
- `#backlog`
- `#blocked`
