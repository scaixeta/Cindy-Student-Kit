# OlaCindyKB — Guia Completo de Uso e Treinamento

> Documento de referência para quem deseja entender, operar ou derivar projetos com a Cindy e a doutrina DOC2.5.

---

## 0. Pré-requisitos e Primeiro Uso

### 0.1 Dependências Locais

| Item | Obrigatório? | Uso |
|---|---|---|
| **Windows** + **PowerShell** | ✅ Sim | Base do ambiente |
| **Git** | ✅ Sim | Versionamento |
| **VSCode** | ✅ Sim | Editor principal |
| **Node.js LTS + npm** | ✅ Sim | `Codex CLI` e projetos JS/TS |
| **Python 3.11+** | ✅ Sim | Projetos Python e utilitários locais |
| **WSL2** | ⬜ Recomendado | Melhor compatibilidade do `Codex` no Windows |

### 0.2 Extensões VSCode Essenciais

Use pelo menos uma superfície de agente. Você pode manter várias instaladas, mas a Cindy não depende de todas ao mesmo tempo.

| Ferramenta | ID / Forma | Essencial quando |
|---|---|---|
| **Cline** | `saoudrizwan.claude-dev` | você opera a Cindy pelo Cline |
| **Codex** | extensão `Codex` ou `Codex CLI` | você opera a Cindy pelo Codex |
| **GitHub Copilot** | `github.copilot` | você usa sugestões inline |
| **GitHub Copilot Chat** | `github.copilot-chat` | você usa chat/agent mode |
| **GitHub Pull Requests and Issues** | `github.vscode-pull-request-github` | seu fluxo usa GitHub |
| **GitLab Workflow** | `GitLab.gitlab-workflow` | seu fluxo usa GitLab |
| **GitLens** | `eamodio.gitlens` | você quer apoio de histórico/revisão |
| **Live Preview** | extensão de preview local | você precisa abrir HTML local rapidamente |
| **Markdown Preview** | nativo do VSCode | você revisa docs `.md` da Cindy |

Observação curta:

- `Cline` é essencial para o fluxo `Cline`.
- `Codex` não depende de extensão obrigatória se você usar o terminal com `Codex CLI`.
- `Copilot Studio` não é requisito base da Cindy no VSCode; trate como ferramenta complementar.

### 0.3 Instalação Rápida

```powershell
winget install Git.Git
winget install Microsoft.VisualStudioCode
winget install OpenJS.NodeJS.LTS
winget install Python.Python.3.12
```

Se for usar `Codex` local no Windows:

```powershell
wsl --install
npm install -g @openai/codex
codex --login
```

Extensões mais comuns:

```powershell
code --install-extension saoudrizwan.claude-dev
code --install-extension github.copilot
code --install-extension github.copilot-chat
code --install-extension github.vscode-pull-request-github
code --install-extension GitLab.gitlab-workflow
code --install-extension eamodio.gitlens
```

### 0.4 Primeiro Uso

```powershell
git clone https://github.com/scaixeta/Cindy-Student-Kit.git C:\MeuProjeto
code C:\MeuProjeto
```

Depois escolha o runtime:

- `Cline`: abra a sidebar do Cline e cole o `Prompt.md`
- `Codex`: abra o terminal integrado e execute `codex`
- `Copilot`: abra o chat do Copilot e use o `Prompt.md`

### 0.5 Comandos PowerShell Essenciais

| Comando | O que faz | Exemplo |
|---|---|---|
| `Get-ChildItem` | Lista arquivos e pastas | `Get-ChildItem C:\MeuProjeto` |
| `Get-Content` | Lê conteúdo de arquivo | `Get-Content README.md` |
| `Set-Location` | Navega entre pastas | `Set-Location C:\MeuProjeto` |
| `New-Item` | Cria arquivo ou pasta | `New-Item -ItemType Directory -Path docs` |
| `Copy-Item` | Copia arquivo ou pasta | `Copy-Item -Recurse rules\ destino\` |
| `Remove-Item` | Remove arquivo ou pasta | `Remove-Item arquivo.txt` |
| `Select-String` | Busca texto em arquivos | `Select-String -Path *.md -Pattern "TODO"` |
| `git status` | Status do repositório | `git status` |
| `git add -A` | Adiciona tudo ao stage | `git add -A` |
| `git commit -m ""` | Faz commit | `git commit -m "mensagem"` |
| `git push` | Envia ao GitHub | `git push` |

---

## 1. O que é a Cindy?

A **Cindy** é uma base portável de governança, contexto e execução para agentes de IA. Ela não é um produto final — é a **fundação** que garante consistência, rastreabilidade e qualidade quando agentes (Cline, Codex, Antigravity ou outros) operam em repositórios.

Pense na Cindy como o **sistema operacional do seu repositório** para agentes:

- Define **regras** que os agentes devem seguir
- Organiza **skills** (capacidades reutilizáveis)
- Mantém **templates** para geração de documentação
- Rastreia **sprints** com timestamps e backlog
- Registra **bugs e testes** com evidências
- Aplica **gates** de aprovação antes de alterar qualquer coisa

---

## 2. Conceitos Fundamentais

### 2.1 A Doutrina DOC2.5

DOC2.5 é o conjunto de regras e práticas que a Cindy segue. Os princípios centrais são:

| Princípio | Significado |
|---|---|
| **Zero Trust** | Nenhuma ação destrutiva sem aprovação do PO |
| **Plano antes de execução** | O agente propõe, o PO aprova |
| **Uma sprint ativa por vez** | Foco e rastreabilidade |
| **Evidência > Inferência** | Fatos observáveis prevalecem |
| **Menor mudança necessária** | Não expandir escopo sem gate |
| **Commit apenas por ordem** | Nunca sugerir commit espontaneamente |

### 2.2 Quem é o PO (Product Owner)?

O PO é **você** — o ser humano que opera com a Cindy. O PO é quem:

- Aprova planos antes da execução
- Autoriza commits e push
- Encerra sprints
- Confirma decisões que viram verdade canônica
- Define escopo e limites

### 2.3 O que são Orchestrators?

Orchestrators são os runtimes de agente que a Cindy suporta:

| Orchestrator | Diretórios | Superfície |
|---|---|---|
| **Cline** | `.clinerules/`, `.cline/skills/` | VSCode |
| **Codex** | `.codex/rules/`, `.codex/skills/` | CLI |
| **Antigravity** | `.agents/rules/`, `.agents/skills/` | VSCode/CLI |

Cada orchestrator tem seus próprios diretórios de regras e skills, mas todos seguem a mesma doutrina DOC2.5 e compartilham a mesma source of truth canônica.

---

## 3. Estrutura do Repositório

### 3.1 Visão Geral

```
Cindy/
├── README.md                  # Entry point oficial
├── Cindy_Contract.md          # Contrato canônico de descoberta
├── Prompt.md                  # Template canônico para bootstrap de novos projetos
├── Dev_Tracking.md            # Índice mestre de sprints
├── Dev_Tracking_SX.md         # Sprint ativa (ex: Dev_Tracking_S2.md)
├── OlaCindyKB.md              # Este guia
├── rules/
│   └── WORKSPACE_RULES.md     # Fonte operacional obrigatória (25 regras)
├── docs/
│   ├── SETUP.md               # Preparação do ambiente
│   ├── ARCHITECTURE.md        # Arquitetura conceitual
│   ├── DEVELOPMENT.md         # Fluxo de desenvolvimento
│   └── OPERATIONS.md          # Operação e governança
├── Templates/
│   ├── README.md              # Template de README para projetos derivados
│   ├── SETUP.md               # Template de docs/SETUP.md
│   ├── ARCHITECTURE.md        # Template de docs/ARCHITECTURE.md
│   ├── DEVELOPMENT.md         # Template de docs/DEVELOPMENT.md
│   ├── OPERATIONS.md          # Template de docs/OPERATIONS.md
│   ├── Dev_Tracking.md        # Template de índice mestre
│   ├── Dev_Tracking_SX.md     # Template de sprint
│   └── bugs_log.md            # Template de log de bugs
├── tests/
│   └── bugs_log.md            # Log centralizado de bugs e testes
├── Sprint/                    # Sprints encerradas (ex: Sprint/Dev_Tracking_S1.md)
├── .agents/                   # Skills canônicas (source of truth)
│   ├── rules/
│   └── skills/
├── .cline/                    # Runtime Cline
│   └── skills/
├── .clinerules/               # Regras e workflows do Cline
│   ├── WORKSPACE_RULES_GLOBAL.md
│   ├── workflows/
│   └── templates/
├── .codex/                    # Runtime Codex
│   ├── rules/
│   └── skills/
└── .brand/
    └── Cindy.jpg              # Imagem oficial da Cindy
```

### 3.2 Papéis de Cada Arquivo

| Arquivo | Papel | Quando Ler |
|---|---|---|
| `rules/WORKSPACE_RULES.md` | Fonte operacional obrigatória. **Prevalece sobre tudo.** | Sempre, antes de qualquer ação |
| `Cindy_Contract.md` | Contrato de descoberta: como o agente identifica runtime, skills e gates | Ao iniciar conversa nova |
| `README.md` | Entry point do repositório. Resumo do estado atual | Ao iniciar conversa nova |
| `Dev_Tracking.md` | Índice mestre: lista de sprints e registros históricos | Ao verificar estado do projeto |
| `Dev_Tracking_SX.md` | Sprint ativa: backlog, decisões, timestamps | Ao trabalhar na sprint |
| `tests/bugs_log.md` | Log de bugs e testes por sprint | Ao registrar ou consultar bugs |
| `Templates/` | Modelos para gerar documentação em projetos novos | Ao fazer bootstrap |
| `Prompt.md` | Template canônico de prompt para criar novos projetos | Ao criar projetos derivados |

---

## 4. Como a Cindy Funciona na Prática

### 4.1 Fluxo de Inicialização (Entry Flow)

Quando um agente (Cline, Codex ou Antigravity) abre uma conversa nova em um workspace Cindy, ele deve seguir este fluxo:

```
1. Ler rules/WORKSPACE_RULES.md
2. Identificar o orchestrator ativo (Cline? Codex? Antigravity?)
3. Ler a regra global do runtime ativo
4. Classificar o workspace:
   - "repo materializado" → já tem README, docs, tracking
   - "baseline de geração" → tem Templates mas não tem docs finais
5. Consultar o skill registry
6. Validar os gates obrigatórios
7. Propor plano ao PO
```

Este fluxo é implementado pela skill `doc25-init`.

### 4.2 O que são Skills?

Skills são **capacidades reutilizáveis** organizadas em pastas com um arquivo `SKILL.md`. Cada skill tem:

- `name:` — identificador
- `description:` — quando usar a skill
- Instruções detalhadas de execução

Exemplo de estrutura:

```
.agents/skills/project-bootstrap/
├── SKILL.md
└── references/
    └── template-field-guide.md
```

### 4.3 Skills Mais Importantes

| Skill | Quando Usar |
|---|---|
| `doc25-init` | Ao iniciar conversa nova ou trocar de escopo |
| `doc25-context-check` | Antes de expandir leitura de contexto |
| `project-bootstrap` | Para criar um projeto novo a partir dos Templates |
| `doc25-commit-gate` | Quando o PO autorizar commit/push |
| `doc25-governance` | Para aplicar guardrails de governança |
| `doc25-dev-workflow` | Para executar tarefas de desenvolvimento na sprint |
| `doc25-preflight` | Antes de alegar conformidade ou conclusão |

### 4.4 O que são Workflows?

Workflows são **prompts salvos como Markdown** em `.clinerules/workflows/`. Diferente de skills (que são pastas com instruções), workflows são arquivos `.md` acionados explicitamente.

Exemplos:
- `init.md` — fluxo de inicialização DOC2.5
- `docs-doc25.md` — fluxo para criar/atualizar documentação canônica

### 4.5 Precedência de Regras

Quando houver conflito, esta é a ordem de precedência:

```
1. rules/WORKSPACE_RULES.md          ← SEMPRE PREVALECE
2. Regra global do runtime ativo
3. Cindy_Contract.md
4. README.md
5. Dev_Tracking.md e sprint ativa
```

---

## 5. Sprints e Rastreabilidade

### 5.1 Como Funciona o Tracking

A Cindy usa um modelo simples de sprints:

- **`Dev_Tracking.md`** — Índice mestre (lista de todas as sprints)
- **`Dev_Tracking_SX.md`** — Sprint ativa (ex: `Dev_Tracking_S2.md`)
- **`Sprint/`** — Pasta para sprints encerradas

Apenas **uma sprint ativa** pode existir na raiz por vez.

### 5.2 Backlog

O backlog usa tabela simples:

```
| Status | Estoria |
|---|---|
| To-Do  | ST-S2-01 - Descrição da tarefa |
| Doing  | ST-S2-02 - Descrição da tarefa |
| Done   | ST-S2-03 - Descrição da tarefa |
```

Estados permitidos: `To-Do`, `Doing`, `Done`, `Accepted`, `Pending-SX`

### 5.3 Decisões

Decisões são registradas no formato:

```
[D-S2-01] - Descrição da decisão
  - Impacto: Alto/Médio/Baixo
  - Arquivos afetados: lista
```

### 5.4 Timestamp UTC (ISO 8601)

O formato canônico de timestamp DOC2.5 é **ISO 8601 com sufixo**:

```
YYYY-MM-DDTHH:MM:SS-ST    (Start)
YYYY-MM-DDTHH:MM:SS-FN    (Finish)
```

Exemplo na tabela:

```
Event | Start | Finish | Status
---|---|---|---
ST-S2-01 | 2026-03-17T21:04:51-ST | 2026-03-17T21:15:00-FN | Done
D-S2-01  | 2026-03-17T21:15:00-ST | 2026-03-17T21:16:00-FN | Logged
```

> **Importante:** Este formato foi adotado na Sprint S2 em substituição ao formato compacto anterior (`DDDMMDDYYYYHHMMSSAM/PMST`), que era ambíguo para LLMs. Dados históricos podem conter o formato legado.

---

## 6. Como Criar um Novo Projeto (Bootstrap)

### 6.1 Pré-requisitos

Para criar um novo projeto derivado da Cindy, você precisa de:

1. Um diretório com a estrutura base da Cindy (rules, Templates, Cindy_Contract.md)
2. O `Prompt.md` da raiz da Cindy

### 6.2 Passo a Passo

**Passo 1: Copiar a base**

Copie os diretórios essenciais da Cindy para o novo workspace:

```powershell
# Criar diretório do novo projeto
New-Item -ItemType Directory -Path "C:\MeuProjeto"

# Copiar a base
Copy-Item -Recurse C:\Cindy\rules        C:\MeuProjeto\rules
Copy-Item -Recurse C:\Cindy\Templates    C:\MeuProjeto\Templates
Copy-Item -Recurse C:\Cindy\.agents      C:\MeuProjeto\.agents
Copy-Item -Recurse C:\Cindy\.cline       C:\MeuProjeto\.cline
Copy-Item -Recurse C:\Cindy\.clinerules  C:\MeuProjeto\.clinerules
Copy-Item -Recurse C:\Cindy\.codex       C:\MeuProjeto\.codex
Copy-Item -Recurse C:\Cindy\.brand       C:\MeuProjeto\.brand
Copy-Item          C:\Cindy\Cindy_Contract.md C:\MeuProjeto\
```

**Passo 2: Copiar e adaptar o Prompt.md**

```powershell
Copy-Item C:\Cindy\Prompt.md C:\MeuProjeto\Prompt.md
```

Edite o `Prompt.md` e substitua `{{PROJECT_GOAL}}` pelo objetivo real do projeto.

**Passo 3: Executar o prompt no agente**

Abra o workspace `C:\MeuProjeto` no editor com seu agente preferido (Cline, Codex ou Antigravity) e cole o conteúdo do `Prompt.md` como primeira instrução.

O agente vai:
1. Ler as rules e o contrato
2. Classificar como `baseline de geração`
3. Apresentar um plano e pedir aprovação
4. Gerar os 8 artefatos canônicos (README, docs, tracking, bugs_log)
5. Validar a saída com score de qualidade

**Passo 4: Verificar a saída**

Confira:
- [ ] 8 arquivos criados?
- [ ] Timestamps no formato ISO 8601?
- [ ] Sem comandos Bash (apenas PowerShell)?
- [ ] Rodapé Cindy copiado literalmente?
- [ ] `Pendente de validação` onde não há dados?

### 6.3 O que o Prompt.md Inclui

O `Prompt.md` canônico contém **3 reminders** obrigatórios que previnem bugs comuns:

1. **Timestamp ISO 8601** — Evita formatos inventados
2. **PowerShell-only** — Evita `ls`, `cd`, `cat`, `bash`
3. **Rodapé limpo** — Evita incluir comentários HTML internos

Estes reminders foram validados em 2 rodadas de teste (Rodada 1: score 72 → Rodada 2: score 92).

---

## 7. Gates Obrigatórios

### 7.1 Quando Pedir Aprovação?

| Situação | Gate |
|---|---|
| Antes de executar uma mudança estrutural | Plano + aprovação do PO |
| Antes de criar ou remover arquivos | Confirmação do PO |
| Antes de `git commit` ou `git push` | Ordem **expressa** do PO |
| Antes de alegar conformidade ou conclusão | `doc25-preflight` |
| Antes de encerrar sprint | **Somente** o PO pode encerrar |

### 7.2 O que o Agente pode Fazer Sozinho?

Comandos de **leitura** são seguros e podem ser executados automaticamente:

- `git status`, `git log`, `git show`, `git branch`
- Leitura de arquivos
- `Get-ChildItem`, `Get-Content`, `Select-String`

---

## 8. Sistema de Qualidade

### 8.1 Score de Qualidade

Toda execução de bootstrap ou ajuste estrutural deve produzir uma avaliação interna de 0 a 100:

| Score | Classificação |
|---|---|
| 0-49 | Ruim — não conforme |
| 50-79 | Parcial — não aprovado |
| **80-100** | **Aprovado** |

O agente **não pode reportar conclusão satisfatória** se o score estiver abaixo de 80.

### 8.2 Budget Contextual

O agente deve trabalhar com **até 30% do contexto disponível**. Se projetar passar disso, deve:

- Resumir o contexto
- Reduzir leitura
- Evitar expandir escopo

### 8.3 Evidência vs. Inferência

| Tipo | Tratamento |
|---|---|
| **Evidência** (fato observável) | Registrar como verdade |
| **Inferência** (conclusão lógica) | Rotular explicitamente como inferência |
| **Pendente** (sem dados suficientes) | Marcar como `Pendente de validação` |
| **Confirmação do PO** | Prevalece sobre inferências |

---

## 9. Portabilidade de Skills

### 9.1 Modelo de Espelhamento

A arquitetura de skills usa 3 camadas:

```
.agents/skills/    ← Source of Truth (autoria canônica)
.cline/skills/     ← Runtime counterpart do Cline
.codex/skills/     ← Runtime counterpart do Codex
```

- A autoria de skills novas ocorre em `.agents/skills/`
- `.cline/` e `.codex/` são espelhos adaptados ao runtime
- Adaptações de runtime são permitidas quando não alteram a governança

### 9.2 Anatomia de uma Skill

```markdown
---
name: nome-da-skill
description: Quando usar esta skill (trigger)
---

# Instruções detalhadas aqui

1. Passo 1
2. Passo 2
3. Passo 3
```

O frontmatter (`name:` e `description:`) é **obrigatório** para discovery.

---

## 10. Bugs e Testes

### 10.1 Registro de Bugs

Formato:

```
- BUG-SX-YY — Título do bug
  - Evidência: o que foi observado
  - Impacto: Alto/Médio/Baixo
  - Referências: arquivos afetados
  - Status: Corrigido / Em aberto
```

### 10.2 Registro de Testes

Formato:

```
- TEST-SX-YY — Título do teste
  - Escopo: o que foi validado
  - Resultado: Aprovado / Reprovado
  - Status: Verde - Aprovado / Vermelho - Reprovado
```

### 10.3 Centralização

Todos os bugs e testes ficam em **`tests/bugs_log.md`**, organizados por sprint. O `Dev_Tracking_SX.md` da sprint ativa contém apenas **resumos e referências cruzadas**.

---

## 11. Segurança

- **Nunca** versionar credenciais
- **Nunca** documentar segredos
- **Mascarar** valores sensíveis
- **Não presumir** `.env` ou storage de secrets sem evidência

---

## 12. Plataforma

A Cindy opera em **ambiente Windows**. Nos documentos e exemplos:

| ✅ Use | ❌ Nunca use |
|---|---|
| `Get-ChildItem` | `ls` |
| `Get-Content` | `cat` |
| `Set-Location` | `cd` |
| `New-Item` | `mkdir`, `touch` |
| `Remove-Item` | `rm` |
| `Select-String` | `grep` |
| Blocos `powershell` | Blocos `bash` |

> **Atenção:** `mkdir -p` em Windows cria uma pasta chamada `-p`. Nunca usar.

---

## 13. Lições Aprendidas

### 13.1 O Bug do Timestamp

O formato compacto original (`DDDMMDDYYYYHHMMSSAM/PMST`) era ambíguo:
- `MM` aparecia 2 vezes (mês e minuto)
- Sem separadores
- AM/PM adicionava complexidade

LLMs geravam formatos híbridos inventados. Foi corrigido na Sprint S2 para **ISO 8601** (`YYYY-MM-DDTHH:MM:SS-ST/FN`).

### 13.2 Reminders no Prompt

Quando um formato é crítico, adicionar **reminders explícitos no Prompt.md** junto com as rules e os templates é mais confiável do que depender apenas de um deles isoladamente.

### 13.3 Teste em 2 Rodadas

O fluxo ideal para validar mudanças na Cindy:

1. **Rodada 1:** Executar com as mudanças e identificar bugs
2. **Corrigir** os bugs encontrados
3. **Rodada 2:** Re-executar e confirmar score >= 80

---

## 14. Referências Rápidas

| Preciso... | Leia... |
|---|---|
| Entender as regras | `rules/WORKSPACE_RULES.md` |
| Ver o estado do projeto | `README.md` |
| Saber como o agente descobre o contexto | `Cindy_Contract.md` |
| Criar um projeto novo | `Prompt.md` + skill `project-bootstrap` |
| Iniciar uma conversa nova | Skill `doc25-init` |
| Verificar conformidade | Skill `doc25-preflight` |
| Registrar um bug | `tests/bugs_log.md` |
| Ver a sprint ativa | `Dev_Tracking_SX.md` na raiz |
| Ver o histórico de sprints | `Dev_Tracking.md` |
| Entender a arquitetura | `docs/ARCHITECTURE.md` |
| Ver como operar o projeto | `docs/OPERATIONS.md` |

---

*Este repositório é orquestrado pela Cindy sob a doutrina DOC2.5.*
