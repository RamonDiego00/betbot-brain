# BetBot Documentation Hub

Central de documentacao operacional para agentes, backlog e decisoes tecnicas.

## Navegacao rapida
- [[Agents/README|Agents]]
- [[Tasks/README|Tasks]]
- [[RFCs/README|RFCs]]
- [[Standards/Task-Standard|Task Standard]]
- [[Standards/RFC-Standard|RFC Standard]]
- [[Standards/Linking-Convention|Linking Convention]]

## Visoes de trabalho
- Backlog ativo: [[Tasks/TODO]]
- Em execucao: [[Tasks/DOING]]
- Em revisao: [[Tasks/REVIEW]]
- Bloqueadas: [[Tasks/BLOCKED]]
- Concluidas: [[Tasks/DONE]]

## Regras obrigatorias
1. Nenhuma execucao de agente sem `task_id` valido.
2. Toda task deve ter `owner_role` definido.
3. Mudancas arquiteturais ou de contrato exigem RFC vinculada.
4. Toda entrega registra log de execucao e hand-off na task.
