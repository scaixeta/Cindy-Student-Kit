# Cindy — Student Kit

> Kit básico para começar a usar a Cindy e a doutrina DOC2.5 em seus projetos.

<p align="center">
  <img src=".brand/Cindy.jpg" alt="Cindy — Agent Orchestrator" width="420" />
</p>

## O que é isto?

Este repositório contém o **kit de partida** da Cindy — uma base portável de governança, contexto e execução para agentes de IA (Cline, Codex, Antigravity).

Com este kit você pode:

- **Criar projetos novos** com estrutura canônica DOC2.5
- **Usar 107+ skills** pré-configuradas para os agentes
- **Manter rastreabilidade** com sprints, timestamps e backlog
- **Aplicar governança** com gates de aprovação e evidências

## Como Começar

### 1. Clone este repositório

```powershell
git clone https://github.com/scaixeta/Cindy-Student-Kit.git C:\MeuProjeto
code C:\MeuProjeto
```

### 2. Leia o guia de treinamento

Abra o **[OlaCindyKB.md](OlaCindyKB.md)** — é o guia completo com:

- Pré-requisitos (software, extensões, API keys)
- Como a Cindy funciona
- Skills e workflows disponíveis
- Como criar projetos novos
- Gates obrigatórios e sistema de qualidade

### 3. Use o Prompt.md

O **[Prompt.md](Prompt.md)** é o template canônico para bootstrap de novos projetos.

1. Abra o `Prompt.md`
2. Substitua `{{PROJECT_GOAL}}` pelo objetivo do seu projeto
3. Cole no agente (Cline, Codex ou Copilot)
4. Aprove o plano quando apresentado
5. O agente gera automaticamente os 8 artefatos canônicos

## Conteúdo do Kit

| Item | Descrição |
|---|---|
| `OlaCindyKB.md` | Guia completo de uso e treinamento |
| `Prompt.md` | Template de bootstrap para novos projetos |
| `Cindy_Contract.md` | Contrato canônico de descoberta dos agentes |
| `rules/` | Regras operacionais DOC2.5 (25 regras) |
| `Templates/` | 8 templates para geração de documentação |
| `.agents/skills/` | 107+ skills canônicas (source of truth) |
| `.cline/skills/` | Skills do runtime Cline |
| `.codex/skills/` | Skills do runtime Codex |
| `.clinerules/` | Regras globais e workflows DOC2.5 |
| `.brand/` | Identidade visual da Cindy |
| `tests/bugs_log.md` | Template de log de bugs e testes |

## Leitura Recomendada

1. **[OlaCindyKB.md](OlaCindyKB.md)** — Guia de treinamento (comece aqui)
2. **[Prompt.md](Prompt.md)** — Template de bootstrap
3. **[rules/WORKSPACE_RULES.md](rules/WORKSPACE_RULES.md)** — Regras operacionais
4. **[Cindy_Contract.md](Cindy_Contract.md)** — Contrato de descoberta

---

## Cindy — Orquestradora (Context Router)

A Cindy é a Orquestradora principal. Em cada run, ela identifica o agente local ativo (Cline/Codex/Antigravity), a superfície de execução (VSCode/CLI) e o workspace root; em seguida, descobre e seleciona as skills/rules disponíveis, respeitando os gates DOC2.5 (plano aprovado antes de execução; commit/push apenas sob ordem explícita do PO).

<p align="center">
  <img src=".brand/Cindy.jpg" alt="Cindy — Orquestradora" width="220" />
</p>

*Este repositório é orquestrado pela Cindy sob a doutrina DOC2.5.*
