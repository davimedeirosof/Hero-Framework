# Hero-Framework v2.3

Setup completo e otimizado do Claude Code do Davi Medeiros. 937 commands, 354 agents, 220 skills, 28 hooks, 14 marketplaces, 2 squads de produção, Opensquad multi-agent orchestration, GSD meta-prompting, e muito mais.

## Quick Install

```bash
git clone https://github.com/davimedeirosof/Hero-Framework.git
cd Hero-Framework
./install.sh
```

---

## Versoes do Sistema

### V1 — Estrutura inicial
- 109 slash commands (15 namespaces)
- 16 agentes
- 22 hooks
- 5 marketplaces
- 8 project rules

### V2 — Reconstrucao completa
- 937 slash commands (86 namespaces)
- 344 agentes especializados
- 211 skills
- 28 hooks
- 14 marketplaces
- Opensquad: framework multi-agente
- GSD: meta-prompting integrado

### V2.1 — Expansao de capacidades
- +1 agente: skill-hunter (busca e instala novas skills automaticamente)
- +9 skills: apify, blotato, canva, image-creator, image-fetcher, image-generator, instagram-publisher, opensquad-agent-creator, opensquad-skill-creator
- Painel dinamico com stats atualizados via GitHub Actions
- CLAUDE.md: persona Hero configurada

### V2.2 — Padronizacao de identidade
- Repositorio renomeado para Hero-Framework
- Padronizacao conceitual e de nomenclatura do sistema
- Versionamento automatico a cada push

### V2.3 — Integração opensquad-content-os
- **2 squads de produção completos** integrados de gabrielrbm-prog/opensquad-content-os
  - `rubimfx-content` — 89 arquivos: carrosséis Instagram para @rubimfx (agentes, pipeline, scripts, templates)
  - `rubimfx-video` — 43 arquivos: Reels/TikTok com clone de voz e imagem
- **+13 skills específicas** do squad de vídeo (clone-validator, lip-sync-fix, photo-to-video, quality-gate, recording-guide, voice-training, thumbnail-generator, trending-sounds, cta-optimizer, ab-testing, post-processing, prompt-engineering-video, nano-banana-video-prompts)
- **8 skills globais atualizadas**: apify, blotato, canva, image-creator, image-fetcher, instagram-publisher (+ script publish.js), opensquad-agent-creator, opensquad-skill-creator
- **_opensquad/core atualizado**: architect.agent.yaml, runner.pipeline.md, skills.engine.md, sherlock.prompt.md
- **24 best-practices guides** atualizados (8 disciplinas + 14 plataformas)
- **13 templates HTML de preview** dos estilos visuais adicionados
- README e Dashboard atualizados

---

## Quadro de Componentes por Versao

| Versao | Commands | Agentes | Skills | Hooks | Squads | Destaque |
|--------|----------|---------|--------|-------|--------|----------|
| V1 | 109 | 16 | — | 22 | — | Estrutura base |
| V2 | 937 | 344 | 211 | 28 | — | Reconstrucao completa |
| V2.1 | 937 | 354 | 220 | 28 | — | +9 skills, painel dinamico |
| V2.2 | 937 | 354 | 220 | 28 | — | Identidade padronizada |
| V2.3 | 937 | 354 | 233 | 28 | 2 | +2 squads completos, +13 skills de vídeo, core atualizado |

> **V2.3 — O que foi adicionado:**
> - +2 squads de produção (rubimfx-content: 89 arquivos, rubimfx-video: 43 arquivos)
> - +13 skills específicas de vídeo (clone-validator, lip-sync-fix, photo-to-video, quality-gate, voice-training, thumbnail-generator, trending-sounds, cta-optimizer, ab-testing, post-processing, prompt-engineering-video, nano-banana-video-prompts, recording-guide)
> - 8 skills globais atualizadas (apify, blotato, canva, image-creator, image-fetcher, instagram-publisher, opensquad-agent-creator, opensquad-skill-creator)
> - _opensquad/core atualizado (architect, runner, skills engine, sherlock, 24 best-practices)
> - 13 templates HTML de preview dos estilos visuais

---

## Squads de Produção (v2.3)

Squads são equipes de agentes que trabalham em pipeline para tarefas complexas. Ficam em `squads/`.

### rubimfx-content

**Objetivo:** Produção de carrosséis Instagram para @rubimfx — notícias macro/ICT/SMC
**Agentes (6):** Nara Notícia, Vitor Visual, Iago Instagram, Léo Legenda, Diana Design, Renata Revisão
**Pipeline:** 12 steps (pesquisa → ângulos → design → legenda → revisão → publicação)
**Templates:** 6 estilos visuais + 13 previews HTML (Twitter Dark, Esteter Style, Hollyfield News, Kaique Epic, BrunoGPT Neon, Minimal Clean)

```bash
/opensquad run rubimfx-content
```

### rubimfx-video

**Objetivo:** Reels/TikTok com clone de voz e imagem para @rubimfx
**Agentes (10):** Rex Roteirista, Hugo HeyGen, Elia ElevenLabs, Sam Submagic, Bea B-Roll, Pablo Publisher, Tina Trend, Ana Analytics, Cal Calendar, Rip Repurpose
**Pipeline:** 15 steps (roteiro → voz → clone → edição → legendas → publicação)
**Skills específicas:** 13 skills (clone-validator, lip-sync-fix, photo-to-video, quality-gate, voice-training, etc.)
**Stack:** Nano Banana Pro 2 + HeyGen/Hedra + ElevenLabs + Submagic (~R$350/mês)

```bash
/opensquad run rubimfx-video
```

---

## Skills (220 total)

### Skills globais Opensquad (`skills/`)

| Skill | Tipo | Função |
|-------|------|--------|
| `apify` | mcp | Web scraping e automação (Instagram, YouTube, TikTok, Google) |
| `blotato` | mcp | Publicação multi-plataforma (IG, LinkedIn, Twitter, TikTok, YouTube) |
| `canva` | mcp | Criar, buscar e exportar designs do Canva |
| `image-creator` | mcp | Renderizar HTML/CSS em PNG via Playwright |
| `image-fetcher` | hybrid | Obter assets visuais (web search, screenshot, arquivos) |
| `instagram-publisher` | script | Publicar carrosséis no Instagram via Graph API |
| `opensquad-agent-creator` | prompt | Criar best-practices na biblioteca do core |
| `opensquad-skill-creator` | prompt | Criar novas skills para o sistema |

### Skills específicas do rubimfx-video (`squads/rubimfx-video/skills/`)

| Skill | Função |
|-------|--------|
| `clone-validator` | Checklist frame-a-frame, score mínimo 8/10 |
| `lip-sync-fix` | Correção de lip sync PT-BR com MuseTalk/Wav2Lip |
| `photo-to-video` | Pipeline completo foto clone → vídeo falando |
| `post-processing` | Upscale, skin texture, color grade |
| `quality-gate` | Checklist visual + voz + formato antes de publicar |
| `recording-guide` | Guia de gravação para clone facial IA |
| `voice-training` | Guia de gravação de áudio para clone de voz |
| `thumbnail-generator` | Capas otimizadas para Reels/TikTok |
| `trending-sounds` | Seleção de trilha sonora por tipo de conteúdo |
| `cta-optimizer` | CTAs contextuais por objetivo (save, comment, share) |
| `ab-testing` | Testes A/B de hooks, thumbnails e horários |
| `nano-banana-video-prompts` | Prompts otimizados para fotos que animam bem |
| `prompt-engineering-video` | Prompts de cenários e backgrounds via IA |

### Outras libraries (`skills/`)
- **Learning Network (ln-*):** 50+ skills para documentacao, auditoria, bootstrap, testing, otimizacao
- **Marketing:** copywriting, content strategy, SEO, email marketing, pricing, CRO
- **Opensquad:** multi-agent orchestration framework completo

---

## Opensquad Framework

Framework de orquestração multi-agente integrado ao Claude Code.

```
/opensquad                → Menu principal / onboarding
/opensquad create         → Criar novo squad (Architect configura tudo)
/opensquad run <nome>     → Executar squad existente
/opensquad edit           → Editar configurações de squad
/opensquad dashboard      → Gerar Virtual Office (dashboard 2D)
```

### Agentes especiais do core

| Agente | Função |
|--------|--------|
| **Architect** | Cria squads via linguagem natural (4 fases: discovery → research → extraction → design) |
| **Sherlock** | Investiga perfis de referência (Instagram, YouTube, Twitter/X, LinkedIn) |
| **Pipeline Runner** | Executa squads automaticamente, pausa em checkpoints |

### 24 Best-Practices guides (`_opensquad/core/best-practices/`)

**Disciplinas (8):** copywriting, researching, image-design, review, social-networks-publishing, strategist, technical-writing, data-analysis

**Plataformas (14):** Instagram Feed, Instagram Reels, Instagram Stories, LinkedIn Post, LinkedIn Article, Twitter Post, Twitter Thread, YouTube Script, YouTube Shorts, Email Newsletter, Email Sales, Blog Post, Blog SEO, WhatsApp Broadcast

### MCP Configuration

```json
{
  "playwright": {
    "command": "npx",
    "args": ["@playwright/mcp@latest", "--config", "_opensquad/config/playwright.config.json"]
  }
}
```

> **Importante:** Desabilitar o plugin nativo Playwright do Claude Code — o Opensquad usa servidor próprio.

---

## Namespaces de Commands (916 total)

**Desenvolvimento:**
- `deploy/` — releases, rollbacks, CI/CD, containerization, Kubernetes
- `dev/` — code review, debugging, refactoring, ultra-think, parallel builds
- `docs/` — API docs, architecture, troubleshooting, migration guides
- `performance/` — audit, bundle, caching, CDN, database, monitoring
- `project/` — init, milestones, health checks, PAC (Product as Code)
- `setup/` — environment, linting, formatting, monorepo, database, GraphQL
- `sync/` — GitHub/Linear bidirectional sync, cross-references
- `team/` — standup, sprint planning, retrospectives, workload balancing
- `test/` — comprehensive testing (unit, E2E, visual, load, mutation, property-based)
- `orchestration/` — task orchestration system
- `spec-workflow/` — spec-driven development with parallel tasks

**AI/Reasoning:**
- `boundary/` — knowledge boundary detection, hallucination prevention
- `context/` — prompt optimization for token efficiency
- `memory/` — memory checkpoint, compression, merge, recall, pruning
- `reasoning/` — multi-path reasoning, chain validation, logic vectors
- `semantic/` — semantic tree management
- `wfgy/` — WFGY semantic reasoning formulas

**Marketing (full suite):**
- `mktg-analytics/`, `mktg-audit/`, `mktg-brand/`, `mktg-campaign/`
- `mktg-checklist/`, `mktg-competitor/`, `mktg-content/`, `mktg-crm/`
- `mktg-cro/`, `mktg-growth/`, `mktg-leads/`, `mktg-marketing/`
- `mktg-ops/`, `mktg-pricing/`, `mktg-report/`, `mktg-research/`
- `mktg-sales/`, `mktg-seo/`, `mktg-sequence/`, `mktg-settings/`, `mktg-social/`
- `mktg-training/` (EN, PT-BR, ES, FR, DE, JA, KO, ZH, AR, RU, VI)

**Expert Squads (multi-agent teams):**
- `advisory-board/` — Ray Dalio, Charlie Munger, Naval Ravikant, Peter Thiel...
- `brand-squad/` — David Aaker, Marty Neumeier, Al Ries...
- `c-level-squad/` — CTO, CMO, COO, CIO, CAIO architects
- `claude-code-mastery/` — meta-optimization of Claude Code itself
- `copy-squad/` — Gary Halbert, Eugene Schwartz, David Ogilvy...
- `cybersecurity/` — pentest, recon, incident response, OWASP audit
- `data-squad/` — Sean Ellis, Avinash Kaushik, Peter Fader...
- `design-squad/` — Brad Frost, Dan Mall, UX/UI engineers
- `hormozi-squad/` — Alex Hormozi business frameworks
- `movement/` — movement building, manifestos, identity creation
- `storytelling/` — Joseph Campbell, Nancy Duarte, Blake Snyder...
- `traffic-masters/` — paid media experts, ad account auditing

**Domain-specific:**
- `media/` — video frame extraction, ElevenLabs transcription
- `rust/` — Rust architecture audits, Tauri MCP integration
- `simulation/` — business scenarios, digital twins, decision trees
- `svelte/` — Svelte 5+ development, Storybook, testing
- `skills/` — skill builder, packager, validator
- `session/` — handoff documents for session continuity
- `webmcp/` — WebMCP tool creation and management

---

## 245 Agentes

Agentes especializados cobrindo todas as areas:
- **Dev:** React, Next.js, Vue, Svelte, Angular, Django, Rails, Spring Boot, Laravel, Flutter, Swift, Kotlin, Rust, Go, C/C++, Elixir
- **Infra:** Kubernetes, Docker, Terraform, AWS/Azure/GCP, CI/CD, SRE
- **Data:** PostgreSQL, database optimization, data engineering, ML/MLOps
- **Security:** penetration testing, security auditing, compliance
- **Business:** product management, project management, UX research
- **Marketing:** SEO, paid media, content, social, email, CRO, analytics
- **China market:** Douyin, Xiaohongshu, WeChat, Baidu, Bilibili, Kuaishou

---

## 28 Hooks

- `gsd-context-monitor.js` — monitoramento de contexto GSD
- `gsd-statusline.js` — status line dinamica
- `gsd-check-update.js` — verificacao de updates GSD
- `pre-compact-save.js` — salva estado antes de compact
- `post-compact-restore.js` — restaura contexto pos-compact
- `context-health-monitor.js` — monitora saude do contexto

---

## Estrutura

```
Hero-Framework/
├── install.sh                  # Script de instalacao
├── settings.json               # Config global (hooks, permissions, marketplaces)
├── CLAUDE.md                   # Persona Hero
├── VERSION                     # Versao atual (2.3)
├── commands/                   # 916 slash commands (86 namespaces)
├── agents/                     # 245 agent personas
├── skills/                     # 220 skill libraries
│   ├── apify/                  # Web scraping (MCP)
│   ├── blotato/                # Publicacao multi-plataforma (MCP)
│   ├── canva/                  # Design Canva (MCP)
│   ├── image-creator/          # HTML → PNG via Playwright (MCP)
│   ├── image-fetcher/          # Assets visuais (hybrid)
│   ├── instagram-publisher/    # Publicacao IG (script Node.js)
│   ├── opensquad-agent-creator/ # Criador de best-practices
│   ├── opensquad-skill-creator/ # Criador de skills
│   └── ln-*/                   # Learning Network (50+ skills)
├── hooks/                      # 28 hook scripts
├── project-rules/              # 8 rules templates
├── _opensquad/                 # Multi-agent orchestration framework
│   ├── core/                   # architect.agent.yaml, runner.pipeline.md, skills.engine.md
│   ├── core/best-practices/    # 24 content guides
│   ├── core/prompts/           # sherlock.prompt.md
│   └── config/                 # Playwright config
├── squads/                     # Squads de producao
│   ├── rubimfx-content/        # Carrosseis Instagram @rubimfx (89 arquivos)
│   │   ├── agents/             # 6 agentes (.agent.md)
│   │   ├── pipeline/           # pipeline.yaml + 12 steps + 7 data files
│   │   ├── scripts/            # 8 scripts Python (clone_image.py, render_slides.py...)
│   │   └── templates/          # 6 estilos visuais + 13 previews HTML
│   └── rubimfx-video/          # Reels/TikTok @rubimfx (43 arquivos)
│       ├── agents/             # 10 agentes (.agent.md)
│       ├── pipeline/           # pipeline.yaml + 15 steps + 5 data files
│       └── skills/             # 13 skills especificas de video
└── docs/                       # Documentacao do framework
    ├── framework/              # opensquad.md, opensquad-core.md, opensquad-skills.md
    └── projetos/               # rubimfx-content-os.md, rubimfx-video-os.md
```

---

## Pos-instalacao

Rodar dentro do Claude Code:

```
/plugin install planning-with-files@planning-with-files
/plugin install claude-hud
/claude-hud:setup
/plugin install oh-my-claudecode
/omc-setup
```

## Ferramentas externas

```bash
# Dippy (auto-approve safe bash commands)
brew tap ldayton/dippy && brew install dippy

# Claude Squad (multi-instance manager)
brew install claude-squad

# parry (prompt injection scanner)
cargo binstall parry-ai
```

## Para projetos

Copie as rules para cada projeto:

```bash
mkdir -p seu-projeto/.claude/rules
cp project-rules/* seu-projeto/.claude/rules/
```

## Variaveis de ambiente necessarias

Para usar as skills de publicação:

```bash
# Instagram Publisher
INSTAGRAM_ACCESS_TOKEN=...
INSTAGRAM_USER_ID=...
IMGBB_API_KEY=...

# Apify (scraping)
APIFY_TOKEN=...

# Blotato (multi-platform publishing)
BLOTATO_API_KEY=...
```
