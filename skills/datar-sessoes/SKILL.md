---
name: datar-sessoes
description: Põe data e hora da última atividade como prefixo [dd/mm HH:mm] no título das sessões do app Claude desktop e atualiza quando mudar. Adds a [dd/mm HH:mm] last-activity timestamp prefix to session titles in the Claude desktop app and refreshes it. Use when the user asks to date sessions, show last-used date, or update session timestamps in the sidebar / quando pedir para datar sessões ou mostrar o último uso.
---

# Datar sessões / Date sessions

Responda no idioma do usuário (pt-BR ou inglês). Reply in the user's language; the steps below are the same in both.

Requer o app Claude desktop (aba Code): usa as ferramentas `mcp__ccd_session_mgmt__list_sessions` e `mcp__ccd_session_mgmt__set_session_title`. Se não estiverem disponíveis (ex.: só terminal), avise e pare.

## Passos

1. Carregue as duas ferramentas com ToolSearch (`select:mcp__ccd_session_mgmt__list_sessions,mcp__ccd_session_mgmt__set_session_title`).
2. Chame `list_sessions` com `limit: 200`. A sessão atual não vem na lista: trate-a à parte com `session_id: "self"` usando `get_session` para ler a data.
3. Para cada sessão, calcule o prefixo `[dd/mm HH:mm]` a partir de `lastActivityAt` (UTC) **convertido para o fuso local do usuário** (ex.: no shell, `date -d "<iso>" "+%d/%m %H:%M"`). Se a data não for do ano corrente, use `[dd/mm/aa HH:mm]`.
4. Novo título = prefixo + espaço + título atual **sem** qualquer prefixo antigo (remova `^\[\d{2}/\d{2}(/\d{2})?( \d{2}:\d{2})?\]\s*`; isso também troca o formato antigo `[dd/mm]`).
5. Pule (e liste no relatório, sem renomear):
   - sessões sem título;
   (Títulos terminados em `…` NÃO são pulados: o app já os grava truncados, e `get_session` devolve o mesmo texto. Verificado em teste.)
   - título já igual ao novo.
6. Antes de renomear em massa, mostre ao usuário a tabela `título atual → novo título` e peça confirmação. Renomeie só depois do sim.
7. Chame `set_session_title` uma vez por sessão. Se o app pedir aprovação, deixe o usuário decidir; não tente contornar.
8. Reporte: quantas renomeadas, quantas puladas e por quê.

## Observações

- A data muda sempre que a sessão tiver atividade nova; rode de novo para atualizar. Para automatizar, o usuário pode criar uma tarefa agendada que invoque `/datar-sessoes`.
- A skill não apaga nem arquiva nada, e só altera títulos.
- Para desfazer: remova o prefixo `[dd/mm] ` de cada título.
