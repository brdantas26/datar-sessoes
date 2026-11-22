# datar-sessoes

🇧🇷 Português abaixo · 🇺🇸 [English version](README.en.md)

Skill para o app **Claude desktop** (aba Code) que coloca a data da última atividade no título de cada sessão: `[22/11 15:14] Dicas do vídeo` (dia/mês hora:minuto). Rode de novo para atualizar as datas.

## Instalar pelo GitHub
```
/plugin marketplace add brdantas26/datar-sessoes
/plugin install datar-sessoes@datar-sessoes
```

## Instalar (local)
Copie a pasta `skills/datar-sessoes` para `~/.claude/skills/` ou carregue a pasta como plugin local. Depois, no app: `/datar-sessoes`.

## Limites
- Só funciona onde existem as ferramentas de sessão do app desktop.
- Não é automático: use uma tarefa agendada que chame `/datar-sessoes` se quiser rodar sozinho.
- Sessões sem título são puladas. Títulos com `…` recebem a data normalmente (o app já os grava truncados).
