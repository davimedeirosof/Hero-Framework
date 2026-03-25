# Opensquad — Orquestração Multi-Agente

## O que é

Sistema que cria e executa squads — equipes de agentes que trabalham em
pipeline para tarefas complexas. Cada agente executa uma etapa e passa
o resultado para o próximo.

## Componentes

| Componente | Arquivo | Função |
|-----------|---------|--------|
| Orquestrador | `_opensquad/core/architect.agent.yaml` | Monta o squad e define o pipeline |
| Pipeline Runner | `_opensquad/core/runner.pipeline.md` | Executa o pipeline passo a passo |
| Skills Engine | `_opensquad/core/skills.engine.md` | Gerencia skills dos agentes |
| Memória | `_opensquad/_memory/` | Contexto persistente entre sessões |

## Fluxo de execução

```
Davi faz uma demanda
  └── Hero recebe e avalia complexidade
        └── Orquestrador monta o squad
              └── Pipeline Runner executa
                    ├── Agente 1 → output 1
                    ├── Agente 2 recebe output 1 → output 2
                    ├── Agente 3 recebe output 2 → output 3
                    └── Resultado final entregue ao Davi
```

## Comandos

```
/opensquad                    → Menu principal / onboarding
/opensquad create             → Criar novo squad (Architect pergunta e configura tudo)
/opensquad run <nome>         → Executar squad existente
/opensquad edit               → Editar configurações de squad
/opensquad help               → Documentação
/opensquad dashboard          → Gerar Virtual Office (dashboard 2D visual)
```

## Squads

Squads ficam em `~/squads/`. Cada squad tem:
- `squad.yaml` — configuração do squad
- `squad-party.csv` — lista de agentes e papéis
- `pipeline/pipeline.yaml` — etapas de execução
- `output/` — resultados por execução (formato: YYYY-MM-DD-HHmmss)
- `_memory/memories.md` — memória do squad

## Squads existentes (Davi)

| Squad | Local | Descrição |
|-------|-------|-----------|
| rubimfx-content | `~/squads/rubimfx-content/` | Carrosséis Instagram macro/ICT para @rubimfx |
| rubimfx-video | `~/squads/rubimfx-video/` | Reels/TikTok com clone de voz e imagem |

## Como iniciar um squad

No Claude Code:
```
/opensquad run rubimfx-content
```

## Arquivos locais

| Caminho | Descrição |
|---------|-----------|
| `~/_opensquad/` | Instalação do Opensquad |
| `~/squads/` | Squads criados |
| `~/_opensquad/_memory/` | Memória global |
| `~/_opensquad/_browser_profile/` | Perfil de browser persistente (sessões Playwright) |
| `~/_opensquad/config/playwright.config.json` | Config do servidor Playwright |

## Virtual Office

Dashboard 2D que mostra agentes trabalhando em tempo real:

```bash
# 1. Gerar dashboard
/opensquad dashboard

# 2. Servir localmente
npx serve squads/<nome-do-squad>/dashboard

# 3. Acessar em
http://localhost:3000
```

## MCP Configuration

O Opensquad usa seu próprio servidor Playwright — **desabilitar o plugin nativo do Claude Code**:

```json
{
  "playwright": {
    "command": "npx",
    "args": ["@playwright/mcp@latest", "--config", "_opensquad/config/playwright.config.json"]
  }
}
```

## Regras críticas

- Não editar `_opensquad/core/` manualmente
- Usar `/opensquad edit` ao invés de editar YAMLs diretamente
- `_opensquad/_memory/company.md` carrega automaticamente a cada execução
- Sessões Playwright em `_browser_profile/` são persistentes e reutilizadas
