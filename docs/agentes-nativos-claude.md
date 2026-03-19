# Agentes Nativos do Claude Code

Estes 5 agentes são built-in do Claude Code (Anthropic).
Não existem como arquivos — são parte do modelo interno.
Não podem ser modificados ou exportados.

---

## 1. general-purpose

**Função:** Agente de uso geral para pesquisas complexas, busca em código e tarefas multi-step.

**Quando é usado:**
- Pesquisas que exigem múltiplas rodadas de busca
- Exploração aberta de codebase sem direção clara
- Tarefas que combinam pesquisa + execução

**Ferramentas disponíveis:** Todas (Glob, Grep, Read, Bash, WebFetch, WebSearch, Write, Edit, etc.)

---

## 2. Explore

**Função:** Exploração rápida de codebases. Especializado em encontrar arquivos por padrão e responder perguntas sobre estrutura de código.

**Quando é usado:**
- Busca de arquivos por padrão (ex: `src/components/**/*.tsx`)
- Busca de keywords no código
- Responder "como X funciona nesse projeto?"

**Níveis de profundidade:** quick / medium / very thorough

**Ferramentas disponíveis:** Todas exceto Agent, ExitPlanMode, Edit, Write, NotebookEdit

---

## 3. Plan

**Função:** Arquiteto de software. Projeta planos de implementação antes de escrever código.

**Quando é usado:**
- Planejar features novas
- Identificar arquivos críticos para uma mudança
- Avaliar trade-offs arquiteturais

**Retorna:** Plano passo a passo, arquivos críticos, considerações de arquitetura

**Ferramentas disponíveis:** Todas exceto Agent, ExitPlanMode, Edit, Write, NotebookEdit

---

## 4. claude-code-guide

**Função:** Especialista em Claude Code CLI, Claude Agent SDK e Claude API (Anthropic).

**Quando é usado:**
- Dúvidas sobre features do Claude Code
- Como usar hooks, slash commands, MCP servers, settings
- Como usar o Anthropic SDK ou Agent SDK

**Ferramentas disponíveis:** Glob, Grep, Read, WebFetch, WebSearch

---

## 5. statusline-setup

**Função:** Configura o status line do Claude Code.

**Quando é usado:**
- Configurar o arquivo `~/.claude/keybindings.json`
- Ajustar o status line exibido na interface

**Ferramentas disponíveis:** Read, Edit

---

## Observações

- Estes agentes são invocados internamente pelo Hero quando necessário
- O usuário não os chama diretamente — o Hero delega para eles
- Não estão no repositório pois são parte do Claude Code (Anthropic)
- Versão documentada em: 2026-03-19
